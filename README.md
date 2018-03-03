# DataBind
Simple data binding for unity.

## Usage
1. Import package file DataBind.unitypackage into Unity
2. Add `DataBindContext` to parent object
3. Add `Bind*` components to children
4. Use `dataBindContext[key] = value` to bind values

Check out Demo/DemoScene for details.

## Bind Text
Surround keys with double curly braces in UI Text and set values in parent `DataBindContext`

![alt text](docs/Component.png)

```csharp
var context = GetComponent<DataBindContext>();
context["Username"] = "Bobby";
```
Result:

![alt text](docs/View.png)

## Custom Binds 
Package contains components for binding UI Text, UI Image's sprite and UI Graphics's color. Custom binds can be created simply by implementing `IBindable` interface.

```csharp
using UnityEngine;
using UnityEngine.UI;

public class BindPosition : MonoBehaviour, IBindable
{
	[SerializeField]
	private Transform m_Target;
	[SerializeField]
	private string m_Key;

	public void Bind(DataBindContext context)
	{
		if (context.ContainsKey(m_Key)) {
			m_Target.position = (Vector3)context[m_Key];
		}
	}
}
```

## Bind any property
You can bind any two properties using `BindProperty` component. Currently, there is no type checking. If destination property is of type `String`, then source will be converted using `ToString` method.

![alt text](docs/BindProperty.png)

## Requirements
TextMeshPro
https://assetstore.unity.com/packages/essentials/beta-projects/textmesh-pro-84126
