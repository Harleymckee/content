
Like our team and process, our stack is constantly evoling. 

We started using react early in its existence.
We have watched the React ecosystem mature.
Ratsnest of Jquery / nilla JS.

Development:
When Revelry began helping companies make technology stack decisions, we typically hooked up our clients with a Ruby/Rails app.

Eventually, Elixir/Beam developed into a production-ready alternative, and when Chris Mccord and friends fabricated the Phoenix web framework, built on the inimitable Elixir database wrapper Ecto, our ears perked up and thoughts of making a change to our base 'stack' started floating. Heralded by Bryan Joseph and Luke Ludet, Elixir started working it's way into our tooling, and after a few mini project pilots, the engineers fell in love with the language (FP/Ruby style/approchable) and managment (and clients) fell in love with the results, we decided to go all in.

We still liked using React but our React projects had gotten a little wacky (make positive). Duplicated state in redux stores. Client side routing on top of. Server side rendering all of this. Too much Javascript can slow down a project. The change to Phoenix gave us the oppurtunity to revauluate how we want to use Javascript and React on our projects.

How? We decided: sparingly.

We have found that, for our typical project, React is best utilized in small doses. We prefer javascripting in the React context to any other JS framework/vanilla, but React code is not immune to 'getting out of hand', not in the slightest. Flux, Redux, React Router, all great open source librarys, but can, especially in the context of a Phoenix web app, end up be misleading and add additonal layers of complexity that are simply not nessisary.

We urge out devs to ask this question and came up with some principles to guide development:
These principles have helped up manage the comlexity of our ever-expanding stock of Elixir/React codebases. These rules are pliable, lodestars whe moving fast and breaking things, that work for us.

First we start with a query, do I need React?

From this question, our core pillars emerge:

PRINCIPLE:
Prefer a request/response over javascript-heavy single page app (SPA).

WHY?
HTML templating (.erb in rails, .eex in Phoenix/Elixir) is typically easier to maintain, faster to load, simpler to optimize,and in the applications native language. Having a Javscript app running in conjunction with a webframework backend is often called (/confused with) and SPA. But unless the client side experience is especially complex (or the application has requirements to meet special cases like the ones listed at the end of this post), this code becomes nothing more than layer of convolution at client. Containers (link), reducers (link), client-side routing (link), do not add a lot of value to a form based CRUD app - why not just send and recieve html if you can get away with it? Html form (in Phoenix the form_for helper) to post and render with response. Simple simple, request/response logic, contained at the controller level, handles how the user interacts with data, without having to build any Javscript machines on the client.

PRINCIPLE:
Prefer native forms over handling http request in javascript

WHY?
HTML forms are simple. Building up ajax requests in JS memory/state is complex. Ajax requests are imperative, and when mixed with client-side state, can cause confusion among developers. Html forms are stateless, simple, declarative, and concise. Ajax requests can be stateful, complex, imperative, and verbose - these four non-qualities are harder to maintain and can rot and accrue tech debt.

PRINCIPLE
Prefer native code (ie .EEx for Elixir) html templating until you cannot.

WHY?
It’s same language as your backend. “EEx stands for Embedded Elixir. It allows you to embed Elixir code inside a string in a robust way” (docs). Write Elixir in html and render is as html with data vs write JS in JSX transpose it to html with data via an Elixir service. The benefits of being able to write Elixir code embedded at template layer go beyond a step off of the UI rendering cycle, Phoenix framework provides many handy helpers and abstraction for common client behavior that, when used correctly, simplify client code dramatically. (talk about and link to LiveView video)

HOW?
Docs for phoenix templates: https://hexdocs.pm/phoenix/templates.html
style using https://github.com/revelrylabs/phoenix_harmonium

However, We still use react. A lot. we still have projects with complext client side interactions that react is well suited for. So its not rare that we come to realize:

I do want/need React

PRINCIPLE:
Prefer sprinkles of React over SPA. What are sprinkles? React components / hierarchy rendered in embedded elixir. When would I need to ‘sprinkle’ when primarily using EEx? When complex interactive components on a page are needed to fill your application requirements, Ie a typeahead dropdown with statful interaction, a complex and stateful calendar component etc. Sprinkles also help manage use of client side apis, ie browser audio and video apis.

WHY?

What is SPA in this context? Heuristic: look for these libraries: Create React App scripts, React Router, Redux, Webpack server. SPAs are not inheritently evil. With Phoenix we could run a client side SPA bundled and served up via webpack and an isolated json REST (or graphql) api, but we lose the aility to write client view related elixir code (EEx), we lose the out of box features of our webframework that promote simplicity, we lose the ability to contain routing lives at Phoenix controller layer (link to redirect helper). We lose helpers for quick wins like flash messages and risk duplicating logic in decoding data over the wire.

HOW?
Render in EEx using https://github.com/revelrylabs/elixir_react_render. This library allows devs to embed react components in EEX templates, render them with the serverside html response, and hydrate the javascript when html response is recieved.

'''—My Project doesn’t follow these principles—'''

Q:
Why would our clients want/have an SPA (or when is SPA kosher)?
A:
If a fully realized http api to a backend application is already built, it is reasonable to make a JS SPA as long as best tools practices are used and with adult supervision.
If GraphQL is used at api layer, it is reasonable to follow JS/React SPA pattern on the front end taking advantage of GraphQL client libraries such as Apollo (https://www.apollographql.com/docs/react/) or Relay (https://facebook.github.io/relay/).
 Also an option to wrap api calls with Elixir/Phoenix app, in which case, see hierarchy above. 

Other special cases:

ReactNative.
Progressive Web Apps.
Zero knowledge Architecture.
