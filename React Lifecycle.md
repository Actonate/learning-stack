## Constructor
- Called only once when component is created
- Send props to base/extended Class i.e. Component (RC)
- Initialize State
- Bind Function Methods

## componentWillMount
- Not really used in real-world applications, you can use constructor instead
- No arguments
- Not recommended to set state, it will delay the page render.
- Not called anytime again in the lifecycle of the component, unless reinstantiated.

## componentDidMount
- Recommended for ASYNC operations like API Calls
- You can setState() in this method, which triggers a re-render.
- Called after the first render function
- Not called anytime again in the lifecycle of the component, unless reinstantiated.

## componentWillUpdate
- Called whenever there are props or state changes
- Called before render (not the initial render);
- DO NOT call this.setState() here #fire.

## componentDidUpdate
- Called whenever there are props or state changes
- Called after render (not the initial render);
- DO NOT call this.setState() here #fire.

## componentWillUnmount
- Called before the component is destroyed
- You cannot do anything to stop the destruction.
- Good place to say your goodbyes, close connections and cleanups (like garbage collection)
- Do not call this.setState here. #genius.

## componentWillReceiveProps
- This is called when the component specifically gets new props (not inner state changes)
- Only parent can change the child's props. #RuleOfTheJungle
- nextProps are available in the first argument which can be checked with this.props for any changes.
- You should use this.setState here to synchronize your state with new props.
- NOT called on initial render.
- Deprecated now, use UNSAFE_componentWillReceiveProps.

## getDerivedStateFromProps
- This is called for each render
- This is a static method, so you cannot access this or this.setState.
- Use props and state in the arguments to access new props and existing state
- Return new state object to change state or return null to avoid changes.



