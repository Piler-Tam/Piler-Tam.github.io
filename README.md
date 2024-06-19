<a name="Dropdown menu with search">
Dropdown menu with search
</a>
Create Dropdown in PropertyDrawer
Remove non-visible characters/Weird string behavior
Fix HDRP UI affected by Anti-Aliasing
TextMeshPro Chinese Font
UnityWebRequest: A Native Collection has not been disposed, resulting in a memory leak.





<h1 id="Dropdown menu with search">
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
