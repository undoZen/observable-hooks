# Suspense

See [Render-as-You-Fetch (using Suspense)](../guide/render-as-you-fetch-suspense.md) for usage.

## ObservableResource

```typescript
Class ObservableResource<TInput, TOutput>
```

<Badge text="v2.2.0"/> Rewires Observable to Relay-like Suspense resource.

**Type parameters:**

- `TInput` Value type of the input Observable.
- `TOutput` Resulted resouce value. Default TInput.

**Constructors**

```typescript
new ObservableResource(
  input$: Observable<TInput>,
  isSuccess?: (value: TInput) => value is TOutput
): ObservableResource
```

**Parameters:**

Name | Type | Description
------ | ------ | ------
`input$` | `Observable<TInput>` | An Observable.
`isSuccess` | `(value: TInput): value is TOutput` | Optional function that determines if the value emitted from `input$` is of success state. If false a Suspense is triggered. Default all true.

**Public Properties:**

Name | Type | Description
------ | ------ | ------
`shouldUpdate$$` | `Subject<undefined>` | Emit when the Component needs extra rerendering.

**Public Methods:**

Name | Type | Description
------ | ------ | ------
`read` | `(): TOutput` | Return cached value on success state. Throw suspender on pending state. Throw error on error state.
`destroy` | `(): void` | UnSubscribe input Observable.

## useObservableSuspense

```typescript
useObservableSuspense<TInput, TOutput>(
  resource: ObservableResource<TInput, TOutput>
): TOutput
```

<Badge text="v2.2.0"/> Consume the Observable resource.

Unlike Promise, Observable implements multiple push protocol.
This hook triggers necessary re-rendering when Suspense should restart.

**Type parameters:**

- `TInput` Value type of the input Observable.
- `TOutput` Resulted resouce value. Default TInput.

**Parameters:**

Name | Type | Description
------ | ------ | ------
`resource` | `ObservableResource<TInput, TOutput>` | Observable resource.

**Returns:**

`TOutput` resouce value.
