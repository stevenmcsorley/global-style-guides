[**↺**BACK](../README.md)

# Jest Guidelines
===

Detailed guidelines on test structure and test definition. This document is aimed at the __Jest__ framework 

https://jestjs.io/docs/en/getting-started

---

## Setup

Creating your test files

### Naming Convention

We should follow a standard pattern for test file names

##### Components

`"ProjectName"-"SectionName"-"ComponentName"`

Example: 

`automation-management-list.spec.ts`

`automation-management-list.snapshots.spec.ts`

_Note:_ We should separate out snap shot tests and unit tests into two separate files

##### Repositories & Services

`"ProjectName"-"ApiName"`

`"ProjectName"-"ServiceName"`

Example: 

`automation-core-api.spec.ts`

`automation-management-service.spec.ts`

### File Structure 

For the component, repositories and service tests the folder structure should mimic the component/class definitions

For other tests we should mimic the same folder structure where possible 

- tests
    - components
        - modules
            - "name of section"
                - "name of component"
                    - snapshots
                    - unit
        - shared
    - helpers
    - repositories
    - services

### Helpers

Any code which is repeated through out the tests should be placed inside a helper file which can be imported into tests.

This keeps the test files clean and has a single source for things like configuration or setup functions

## Test Definition

Tests should be tidy, easy to read and easy to maintain. In order to achieve this we should write each test in the same format.

### Naming Conventions

All tests should follow the name naming convention 

##### Describe (Group Test Name)

The test description should match the folder structure. With an identifer at the start stating which type of test it is
- Snapshot
- Component
- Service
- Repository

`describe('Snapshot: "ProjectName"/"SectionName"/"Component"', () => {})`

`describe('Component: "ProjectName"/"SectionName"/"Component"', () => {})`

`describe('Service: "ProjectName"/Service/"ServiceName"', () => {})`

`describe('Repository: "ProjectName"/Repository/"ApiName"', () => {})`

Example

`describe('Snapshot: Automation/Management/List', () => {})`

`describe('Component: Automation/Management/List', () => {})`

`describe('Service: Automation/Service/Management', () => {})`

`describe('Repository: Automation/Repository/Core', () => {})`

##### It (Single Test Name)

We should define here a brief summary of what the test is executing & asserting. 

This should be short and informative.

Example

`it('should populate rules on create', async() => {})`

`it('should define columns on create ', async() => {})`

`it('should match the snapshot when no data is present', async() => {})`

`it('should match the snapshot when an error occurred loading data', async() => {})`


## Jest API

### Globals

In your test files, Jest puts each of these methods and objects into the global environment. You don't have to require or import anything to use them.

##### Methods
- afterAll(fn, timeout)
- afterEach(fn, timeout)
- beforeAll(fn, timeout)
- beforeEach(fn, timeout)
- describe(name, fn)
- describe.each(table)(name, fn, timeout)
- describe.only(name, fn)
- describe.only.each(table)(name, fn)
- describe.skip(name, fn)
- describe.skip.each(table)(name, fn)
- test(name, fn, timeout)
- test.each(table)(name, fn, timeout)
- test.only(name, fn, timeout)
- test.only.each(table)(name, fn)
- test.skip(name, fn)
- test.skip.each(table)(name, fn)
- test.todo(name)

---

Referer to the link for details on each method 

https://jestjs.io/docs/en/api

---

### Expect (Assertion)

When you're writing tests, you often need to check that values meet certain conditions. 

`expect` gives you access to a number of "matchers" that let you validate different things.

##### Methods

- expect(value)
- expect.extend(matchers)
- expect.anything()
- expect.any(constructor)
- expect.arrayContaining(array)
- expect.assertions(number)
- expect.hasAssertions()
- expect.not.arrayContaining(array)
- expect.not.objectContaining(object)
- expect.not.stringContaining(string)
- expect.not.stringMatching(string | regexp)
- expect.objectContaining(object)
- expect.stringContaining(string)
- expect.stringMatching(string | regexp)
- expect.addSnapshotSerializer(serializer)
- .not
- .resolves
- .rejects
- .toBe(value)
- .toHaveBeenCalled()
- .toHaveBeenCalledTimes(number)
- .toHaveBeenCalledWith(arg1, arg2, ...)
- .toHaveBeenLastCalledWith(arg1, arg2, ...)
- .toHaveBeenNthCalledWith(nthCall, arg1, arg2, ....)
- .toHaveReturned()
- .toHaveReturnedTimes(number)
- .toHaveReturnedWith(value)
- .toHaveLastReturnedWith(value)
- .toHaveNthReturnedWith(nthCall, value)
- .toHaveLength(number)
- .toHaveProperty(keyPath, value?)
- .toBeCloseTo(number, numDigits?)
- .toBeDefined()
- .toBeFalsy()
- .toBeGreaterThan(number | bigint)
- .toBeGreaterThanOrEqual(number | bigint)
- .toBeLessThan(number | bigint)
- .toBeLessThanOrEqual(number | bigint)
- .toBeInstanceOf(Class)
- .toBeNull()
- .toBeTruthy()
- .toBeUndefined()
- .toBeNaN()
- .toContain(item)
- .toContainEqual(item)
- .toEqual(value)
- .toMatch(regexpOrString)
- .toMatchObject(object)
- .toMatchSnapshot(propertyMatchers?, hint?)
- .toMatchInlineSnapshot(propertyMatchers?, inlineSnapshot)
- .toStrictEqual(value)
- .toThrow(error?)
- .toThrowErrorMatchingSnapshot(hint?)
- .toThrowErrorMatchingInlineSnapshot(inlineSnapshot)

---

Referer to the link for details on each method 

https://jestjs.io/docs/en/expect

---


### Mocking

Mock functions are also known as "spies", because they let you spy on the behavior of a function that is called indirectly by some other code, rather than only testing the output. 

You can create a mock function with jest.fn(). 

If no implementation is given, the mock function will return undefined when invoked.

##### Methods

- mockFn.getMockName()
- mockFn.mock.calls
- mockFn.mock.results
- mockFn.mock.instances
- mockFn.mockClear()
- mockFn.mockReset()
- mockFn.mockRestore()
- mockFn.mockImplementation(fn)
- mockFn.mockImplementationOnce(fn)
- mockFn.mockName(value)
- mockFn.mockReturnThis()
- mockFn.mockReturnValue(value)
- mockFn.mockReturnValueOnce(value)
- mockFn.mockResolvedValue(value)
- mockFn.mockResolvedValueOnce(value)
- mockFn.mockRejectedValue(value)
- mockFn.mockRejectedValueOnce(value)

---

Referer to the link for details on each method 

https://jestjs.io/docs/en/mock-function-api

---

Examples of mocks

```typescript
const tableService = jest.fn().mockImplementationOnce(() => 'tableService');
```

```typescript
const container = jest.fn().mockImplementationOnce(() => '');
```

```typescript
component.vm.$store.setConditionParameter = jest.fn();
```

```typescript
  jest.mock('../../../../Repositories/AutomationRuleManagerRepository')

  repository.fetchRuleTypes = jest.fn(() => {
    return Promise.resolve(getMockObjs().ruleTypes)
  })
```

## Test Types

Regardless of the test type with the exclusion of Snapshot testing. 

A test should be written with only 1 purpose. This usually means 1 assertion.

You should be able to describe your test as a single sentence in English

---
I want to test `THAT` _xxx_ `DOES` _xxx_ `WHEN` _xxx_

---



### Snapshot Testing

Snapshot tests are a very useful tool whenever you want to make sure your UI does not change unexpectedly.

A typical snapshot test case for a mobile app renders a UI component, takes a snapshot, then compares it to a reference snapshot file stored alongside the test. The test will fail if the two snapshots do not match: either the change is unexpected, or the reference snapshot needs to be updated to the new version of the UI component.

__*Snapshots should be written in separate files from unit tests__

_This is for ease of maintaining and also it means they can be run in a separate task._

#### Best Practises

__Treat snapshots as code__

Commit snapshots and review them as part of your regular code review process. This means treating snapshots as you would any other type of test or code in your project.

__Tests should be deterministic__

Your tests should be deterministic. Running the same tests multiple times on a component that has not changed should produce the same results every time. You're responsible for making sure your generated snapshots do not include platform specific or other non-deterministic data.

For example, if you have a Clock component that uses Date.now(), the snapshot generated from this component will be different every time the test case is run. In this case we can mock the Date.now() method to return a consistent value every time the test is run:

### Component Testing

Component testing is split into two main parts.

1. DOM Manipulation 
2. Functional 

#### DOM Manipulation 

This is primarily a set of tests to test the user interaction with the component. 

It is usually driven by mouse clicks or mouse actions.

In these tests we simulate these actions using Javascript and test the components response 

We should apply attributes to elements which are used for this purpose

`[data-jest-id='actionId']'` 

_This will prevent tests breaking due to developers changing `ids` or `class` names_

##### Asserting

To keep or tests slim and maintainable we should only test that the desired function is hit with the DOM action or the desired property is updated

We would do this with mocking the function or property. 

By mocking the function we can assert it was called and/or called with the correct parameters

#### Functional

This comes hand in hand with the approach stated above.

At this level of testing we should test every potential code path of a function.

We should be testing and asserting the response/output of the function

---
`WHEN` I call _xxx_ `WITH` _xxx_ `THEN` _xxx_

---

_Note:_ It is important that we test both valid cases and invalid cases. 

#### Provide & Inject

This pair of options are used together to allow an ancestor component to serve as a dependency injector for all its descendants, regardless of how deep the component hierarchy is, as long as they are in the same parent chain. 

This is essentially dependency injections for Vue

The provide option should be an object or a function that returns an object. 

This object contains the properties that are available for injection into its descendants. 

The standard Provide & Inject are __NOT__ reactive how ever a 3rd party library can be used in conjunction to have __reactive__ provides & injects

#### Testing with Provide & Inject

When mounting you component you must declare a _provide_ object and an _inject_ array in the options 

---
_Example_
```typescript
const options: any = {
  provide: {
    container: diContainer,
    settings: appSettings
  },
  inject: ['container', 'settings']
}
```


These can either be concrete implementations of mocked functions at this point depending on the test

---

_Mocked Example_
```typescript

const options: any = {
  provide: {
    container: diContainer,
    settings: jest.fn().mockImplementationOnce(() => 'tableSettings')
  },
  inject: ['container', 'settings']
}
```

If your component has reactive provides and injects you need to declare inside the prodive which of the injects are reactive.

Again this can either be concrete implementations or mocks.

---
_Reactive Example_
```typescript
const options: any = {
  provide: {
    container: diContainer,
    settings: appSettings,
    __reactiveInject__: [container, appSettings]
  },
  inject: ['container', 'settings']
}
```

### Unit Testing

Unit testing would be mainly used for services and repositories or any functional helper / classes

The pattern should be almost identical to the component functional testing.

At this level of testing we should test every potential code path of a function.

We should be testing and asserting the response/output of the function

---
`WHEN` I call _xxx_ `WITH` _xxx_ `THEN` _xxx_

---

_Note:_ It is important that we test both valid cases and invalid cases. 

[**⇪**TOP](#jest-guidelines)