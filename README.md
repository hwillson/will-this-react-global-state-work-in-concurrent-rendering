# Will this React global state work in concurrent rendering?

Test tearing and branching in React concurrent rendering

## Introduction

React 18 is coming with a new feature called "concurrent rendering".
With global state, there's a theoretical issue called "tearing"
that might occur in React concurrent rendering.

Let's test the behavior!

## What is tearing?

- [Stack Overflow](https://stackoverflow.com/questions/54891675/what-is-tearing-in-the-context-of-the-react-redux)
- [Talk by Mark Erikson](https://www.youtube.com/watch?v=yOZ4Ml9LlWE&t=933s)
- [Talk by Flarnie Marchan](https://www.youtube.com/watch?v=V1Ly-8Z1wQA&t=1079s)
- Some other resources
  - https://github.com/reactjs/rfcs/pull/147
  - https://gist.github.com/bvaughn/054b82781bec875345bd85a5b1344698

## What is branching?

- Old resources
  - https://reactjs.org/docs/concurrent-mode-intro.html

## How does it work?

A small app is implemented with each library.
The state has one count.
The app shows the count in fifty components.

There's a button outside of React and
if it's clicked it will trigger state mutation.
This is to emulate mutating an external state outside of React,
for example updating state by Redux middleware.

The render has intentionaly expensive computation.
If the mutation happens during rendering with in a tree,
there could be an inconsistency in the state.
If it finds the inconsistency, the test will fail.

## How to run

```bash
git clone https://github.com/dai-shi/will-this-react-global-state-work-in-concurrent-rendering.git
cd will-this-react-global-state-work-in-concurrent-rendering
yarn install
yarn run build-all
yarn run jest
```

## Screencast (old)

<img src="https://user-images.githubusercontent.com/490574/61502196-ce109200-aa0d-11e9-9efc-6203545d367c.gif" alt="Preview" width="350" />

## Test scenario

- with useTransition
  - test 1: updated properly with transition
  - test 2: no tearing with transition
  - test 3: ability to interrupt render
  - test 4: proper branching with transition
- with intensive auto increment (EXPERIMENTAL)
  - test 5: updated properly with auto increment
  - test 6: no tearing with auto increment

## Results

<details>
<summary>Raw Output</summary>

```
  react-redux
    with useTransition
      ✓ test 1: updated properly with transition (2729 ms)
      ✕ test 2: no tearing with transition (52 ms)
      ✓ test 3: ability to interrupt render
      ✕ test 4: proper branching with transition (7164 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (2260 ms)
      ✕ test 6: no tearing with auto increment (1 ms)
  redux-use-mutable-source
    with useTransition
      ✓ test 1: updated properly with transition (2741 ms)
      ✓ test 2: no tearing with transition (122 ms)
      ✓ test 3: ability to interrupt render
      ✕ test 4: proper branching with transition (7536 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (2257 ms)
      ✕ test 6: no tearing with auto increment (1 ms)
  reactive-react-redux
    with useTransition
      ✓ test 1: updated properly with transition (2718 ms)
      ✓ test 2: no tearing with transition (121 ms)
      ✓ test 3: ability to interrupt render
      ✕ test 4: proper branching with transition (7535 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (2241 ms)
      ✕ test 6: no tearing with auto increment (1 ms)
  react-tracked
    with useTransition
      ✓ test 1: updated properly with transition (3585 ms)
      ✓ test 2: no tearing with transition (25 ms)
      ✓ test 3: ability to interrupt render (1 ms)
      ✓ test 4: proper branching with transition (5430 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (6174 ms)
      ✓ test 6: no tearing with auto increment
  constate
    with useTransition
      ✓ test 1: updated properly with transition (2749 ms)
      ✓ test 2: no tearing with transition (48 ms)
      ✓ test 3: ability to interrupt render
      ✓ test 4: proper branching with transition (3415 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (4040 ms)
      ✓ test 6: no tearing with auto increment (1 ms)
  zustand
    with useTransition
      ✓ test 1: updated properly with transition (3580 ms)
      ✓ test 2: no tearing with transition (121 ms)
      ✓ test 3: ability to interrupt render
      ✕ test 4: proper branching with transition (7518 ms)
    with intensive auto increment
      ✕ test 5: updated properly with auto increment (13232 ms)
      ✕ test 6: no tearing with auto increment (5 ms)
  react-hooks-global-state
    with useTransition
      ✓ test 1: updated properly with transition (3467 ms)
      ✓ test 2: no tearing with transition (28 ms)
      ✓ test 3: ability to interrupt render
      ✕ test 4: proper branching with transition (7208 ms)
    with intensive auto increment
      ✕ test 5: updated properly with auto increment (13235 ms)
      ✕ test 6: no tearing with auto increment (19 ms)
  use-context-selector
    with useTransition
      ✓ test 1: updated properly with transition (3586 ms)
      ✓ test 2: no tearing with transition (38 ms)
      ✓ test 3: ability to interrupt render (1 ms)
      ✓ test 4: proper branching with transition (5427 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (6172 ms)
      ✓ test 6: no tearing with auto increment (1 ms)
  use-subscription
    with useTransition
      ✓ test 1: updated properly with transition (3529 ms)
      ✓ test 2: no tearing with transition (121 ms)
      ✓ test 3: ability to interrupt render
      ✕ test 4: proper branching with transition (7534 ms)
    with intensive auto increment
      ✕ test 5: updated properly with auto increment (13238 ms)
      ✕ test 6: no tearing with auto increment (12 ms)
  react-state
    with useTransition
      ✓ test 1: updated properly with transition (2777 ms)
      ✓ test 2: no tearing with transition (61 ms)
      ✓ test 3: ability to interrupt render (1 ms)
      ✓ test 4: proper branching with transition (3392 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (4023 ms)
      ✓ test 6: no tearing with auto increment (1 ms)
  simplux
    with useTransition
      ✓ test 1: updated properly with transition (2833 ms)
      ✓ test 2: no tearing with transition (50 ms)
      ✓ test 3: ability to interrupt render
      ✕ test 4: proper branching with transition (7376 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (4143 ms)
      ✓ test 6: no tearing with auto increment
  react-apollo
    with useTransition
      ✕ test 1: updated properly with transition (6027 ms)
      ✓ test 2: no tearing with transition (59 ms)
      ✕ test 3: ability to interrupt render (2 ms)
      ✕ test 4: proper branching with transition (4606 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (3096 ms)
      ✓ test 6: no tearing with auto increment (1 ms)
  recoil
    with useTransition
      ✕ test 1: updated properly with transition (8594 ms)
      ✓ test 2: no tearing with transition (54 ms)
      ✕ test 3: ability to interrupt render (2 ms)
      ✕ test 4: proper branching with transition (6335 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (4084 ms)
      ✓ test 6: no tearing with auto increment (1 ms)
  jotai
    with useTransition
      ✓ test 1: updated properly with transition (3588 ms)
      ✓ test 2: no tearing with transition (122 ms)
      ✓ test 3: ability to interrupt render
      ✕ test 4: proper branching with transition (7554 ms)
    with intensive auto increment
      ✕ test 5: updated properly with auto increment (13266 ms)
      ✕ test 6: no tearing with auto increment (4 ms)
  effector
    with useTransition
      ✓ test 1: updated properly with transition (2730 ms)
      ✕ test 2: no tearing with transition (51 ms)
      ✓ test 3: ability to interrupt render (1 ms)
      ✕ test 4: proper branching with transition (7219 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (2246 ms)
      ✕ test 6: no tearing with auto increment (1 ms)
  react-rxjs
    with useTransition
      ✕ test 1: updated properly with transition (6019 ms)
      ✓ test 2: no tearing with transition (53 ms)
      ✕ test 3: ability to interrupt render (1 ms)
      ✕ test 4: proper branching with transition (4583 ms)
    with intensive auto increment
      ✓ test 5: updated properly with auto increment (3050 ms)
      ✓ test 6: no tearing with auto increment (2 ms)
  valtio
    with useTransition
      ✓ test 1: updated properly with transition (3509 ms)
      ✓ test 2: no tearing with transition (23 ms)
      ✓ test 3: ability to interrupt render
      ✕ test 4: proper branching with transition (7221 ms)
    with intensive auto increment
      ✕ test 5: updated properly with auto increment (13274 ms)
      ✕ test 6: no tearing with auto increment (2 ms)
```

</details>

<table>
  <tr>
    <th>Test</th>
    <th>1</th>
    <th>2</th>
    <th>3</th>
    <th>4</th>
    <th>5</th>
    <th>6</th>
  </tr>

  <tr>
    <th><a href="https://react-redux.js.org">react-redux</a></th>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
  </tr>

  <tr>
    <th><a href="https://redux.js.org">redux</a> (w/ useMutableSource)</th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/dai-shi/reactive-react-redux">reactive-react-redux</a></th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
  </tr>

  <tr>
    <th><a href="https://react-tracked.js.org">react-tracked</a></th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/diegohaz/constate">constate</a></th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/pmndrs/zustand">zustand</a></th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:x:</td>
    <td>:x:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/dai-shi/react-hooks-global-state">react-hooks-global-state</a></th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:x:</td>
    <td>:x:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/dai-shi/use-context-selector">use-context-selector</a> (w/ useReducer)</th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/facebook/react/tree/master/packages/use-subscription">use-subscription</a> (w/ redux)</th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:x:</td>
    <td>:x:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/MrWolfZ/simplux">simplux</a></th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/apollographql/react-apollo">react-apollo</a></th>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
  </tr>

  <tr>
    <th><a href="https://recoiljs.org">recoil</a></th>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/pmndrs/jotai">jotai</a></th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:x:</td>
    <td>:x:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/zerobias/effector">effector</a></th>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
  </tr>

  <tr>
    <th><a href="https://react-rxjs.org">react-rxjs</a></th>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:x:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
  </tr>

  <tr>
    <th><a href="https://github.com/pmndrs/valtio">valtio</a></th>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:white_check_mark:</td>
    <td>:x:</td>
    <td>:x:</td>
    <td>:x:</td>
  </tr>

</table>

## Caveats

- Tearing may not be an issue depending on app requirements.
- The test is done in a very limited way.
- The results may not be accurate.

## If you are interested

The reason why I created this is to test my projects.

- [react-tracked](https://github.com/dai-shi/react-tracked)
- [reactive-react-redux](https://github.com/dai-shi/reactive-react-redux)
- and so on

## Contributing

This repository is a tool for us to test some of global state libraries.
While it is totally fine to use the tool for other libraries under the license,
we don't generally accept adding a new library to the repository.

However, we are interested in various approaches.
If you have any suggestions feel free to open issues or pull requests.
We may consider adding (and removing) libraries.
Questions and discussions are also welcome in issues.

For listing global state libraries, we have another repository
https://github.com/dai-shi/lets-compare-global-state-with-react-hooks
in which we accept contributions. It's recommended to run this tool
and we put the result there, possibly a reference link to a PR
in this repository or a fork of this repository.
