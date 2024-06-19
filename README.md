<a href="#1">
Dropdown menu with search
</a>

<br/>
<a href="#2">
Create Dropdown in PropertyDrawer
</a>

<br/>
<a href="#3">
Remove non-visible characters/Weird string behavior
</a>

<br/>
<a href="#4">
Fix HDRP UI affected by Anti-Aliasing
</a>

<br/>
<a href="#5">
TextMeshPro Chinese Font
</a>

<br/>
<a href="#6">
UnityWebRequest: A Native Collection has not been disposed, resulting in a memory leak.
</a>



<br/> 
<h1 id="1">
Dropdown menu with search
</h1>

```
using UnityEditor;
using UnityEngine;
using UnityEditor.IMGUI.Controls;

class WeekdaysDropdown : AdvancedDropdown
{
    public WeekdaysDropdown(AdvancedDropdownState state) : base(state)
    {
    }

    protected override AdvancedDropdownItem BuildRoot()
    {
        var root = new AdvancedDropdownItem("Weekdays");

        var firstHalf = new AdvancedDropdownItem("First half");
        var secondHalf = new AdvancedDropdownItem("Second half");
        var weekend = new AdvancedDropdownItem("Weekend");

        firstHalf.AddChild(new AdvancedDropdownItem("Monday"));
        firstHalf.AddChild(new AdvancedDropdownItem("Tuesday"));
        secondHalf.AddChild(new AdvancedDropdownItem("Wednesday"));
        secondHalf.AddChild(new AdvancedDropdownItem("Thursday"));
        weekend.AddChild(new AdvancedDropdownItem("Friday"));
        weekend.AddChild(new AdvancedDropdownItem("Saturday"));
        weekend.AddChild(new AdvancedDropdownItem("Sunday"));

        root.AddChild(firstHalf);
        root.AddChild(secondHalf);
        root.AddChild(weekend);

        return root;
    }
}

public class AdvancedDropdownTestWindow : EditorWindow
{
    void OnGUI()
    {
        var rect = GUILayoutUtility.GetRect(new GUIContent("Show"), EditorStyles.toolbarButton);
        if (GUI.Button(rect, new GUIContent("Show"), EditorStyles.toolbarButton))
        {
            var dropdown = new WeekdaysDropdown(new AdvancedDropdownState());
            dropdown.Show(rect);
        }
    }
}
```

https://docs.unity3d.com/ScriptReference/IMGUI.Controls.AdvancedDropdown.html


<br/> 
<h1 id="2">
Create Dropdown in PropertyDrawer
</h1>

Offical example code:
```
public override void OnGUI(Rect position, SerializedProperty property, GUIContent label)
{
    index = EditorGUILayout.Popup(index, options);
}
```
If you want to update property value after select:
```
public override void OnGUI(Rect position, SerializedProperty property, GUIContent label)
{
  int index = Array.IndexOf(options, property.objectReferenceValue);
  
  if (index!= -1)
  {
      index = EditorGUI.Popup(position, label.text, index, options);
      property.objectReferenceValue = options[index];
  }
}
```


