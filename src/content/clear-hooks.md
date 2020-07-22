---
layout: post
title: Clearing Data in React Hooks
image: img/hooks.jpeg
author: Pranay Aryal
date: 2019-07-10T10:00:00.000Z
tags:
  - React
---

Thanks to this
<a target="_blank" href="https://stackoverflow.com/questions/54895883/reset-to-initial-state-with-react-hooks">StackOverflow Post</a>
The code has been copied from there for quick reference.

Clearing data with React Hooks can be tricky.

Use `useReducer` to clear data.

```js
import React, { useReducer } from "react";

const initialState = {
    username: "",
    email: "",
    password: "",
    passwordConfirmation: "",
};

const reducer = (state, action) => {
    if (action.type === "reset") {
        return initialState;
    }

    const result = { ...state };
    result[action.type] = action.value;
    return result;
};

const Signup = () => {
    const [state, dispatch] = useReducer(reducer, initialState);
    const { username, email, password, passwordConfirmation } = state;

    const handleSubmit = e => {
        e.preventDefault();

        /* fetch api */

        /* clear state */
        dispatch({ type: "reset" });
    };

    const onChange = e => {
        const { name, value } = e.target;
        dispatch({ type: name, value });
    };

    return (
        <form onSubmit={handleSubmit}>
            <div>
                <label>
                    Username:
                    <input value={username} name="username" onChange={onChange} />
                </label>
            </div>
            <div>
                <label>
                    Email:
                    <input value={email} name="email" onChange={onChange} />
                </label>
            </div>
            <div>
                <label>
                    Password:
                    <input
                        value={password}
                        name="password"
                        type="password"
                        onChange={onChange}
                    />
                </label>
            </div>
            <div>
                <label>
                    Confirm Password:
                    <input
                        value={passwordConfirmation}
                        name="passwordConfirmation"
                        type="password"
                        onChange={onChange}
                    />
                </label>
            </div>
            <button>Submit</button>
        </form>
    );
};

export default Signup;
```
