### How react works

1.  React Components have **state**, **props**, **render()** (and sometimes **handleClick**)

    ```JSX
    class Child extends React.Component {
        render () {
            return (
            <div
                className="Child"
                onClick={ this.props.onClick }
            >
                { this.props.value }
            </div>
            )
        };
    }
    ```

    ```JSX
    class Parent extends React.Component {
        constructor (props) {
            this.state = { value: "Hello!" };
        }

        handleClick(){}

        render () {
            return ( <Child value={ this.state.value } onClick={ () => this.handleClick() }/> )
        };
    }
    ```

2.  Parent React Component stores state. Thus it also defines handleClick as this component has access to whole state. It passes down values to Child Components using props
3.  Components that have state initialise it in constructor, thus have constructors.
4.  Components that do not have state can be made into function components instead of class components. Both are given below for comparison:

    ```JSX
    class Child extends React.Component {
      render() {
        return <div> </div>;
      }
    }
    ```

    ```JSX
    function Child(props) {
      return <div> </div>;
    }
    ```

5.  To **lift state up** from an element to new parent element:

    - Make **new state** in **Parent** element's constructor and **remove state from child** element, It will be **passed down using props**
    - **Remove handleClick** from **Child**, because of **2.** This will also be **passed down using props**
    - Everything else remain same

6.  Immutability is important. So do not change state directly.

    - Use **setState** method of component.
    - If there is an array/object in state, first make copy of array/object, modify it then replace in state using setState
    - To add to an array, use concat method instead of push as concat returns a new array and does not modify existing one
