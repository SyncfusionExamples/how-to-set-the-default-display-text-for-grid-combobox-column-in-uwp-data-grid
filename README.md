# How to Set the Default Display Text for GridComboBoxColumn in UWP DataGrid?

This sample illustrates how to set the default display text for [GridComboBoxColumn](https://help.syncfusion.com/cr/uwp/Syncfusion.UI.Xaml.Grid.GridComboBoxColumn.html) in [UWP DataGrid](https://www.syncfusion.com/uwp-ui-controls/datagrid) (SfDataGrid).

In `DataGrid`, `GridComboBoxColumn` does not have direct support to display default text on it when there is no selected Item. You can change default text using ComboBoxValueConverter and DisplayBinding property of the column.

#### XAML
``` xml
<Page.Resources>
    <local:ComboBoxValueConverter x:Key="comboBoxValueConverter"/>
</Page.Resources>
<syncfusion:SfDataGrid Name="dataGrid"
                        AutoGenerateColumns="False"
                        AllowEditing="True"
                        ColumnSizer="Auto"
                        ItemsSource="{Binding Employees}">
    <syncfusion:SfDataGrid.Columns>
        <syncfusion:GridTextColumn MappingName="FirstName" HeaderText="First Neme" ColumnFilter="DisplayText" />
        <syncfusion:GridTextColumn  MappingName="LastName" HeaderText="Last Name" />
        <syncfusion:GridTextColumn MappingName="ID"/>
        <syncfusion:GridTextColumn  MappingName="Title" />
        <syncfusion:GridTextColumn  MappingName="Salary" />
        <syncfusion:GridComboBoxColumn MappingName="ReportsTo" HeaderText="Reports To" ItemsSource="{Binding Reporters}" DisplayBinding="{Binding Path=ReportsTo, Converter={StaticResource comboBoxValueConverter}}"/>
    </syncfusion:SfDataGrid.Columns>
</syncfusion:SfDataGrid>
```

#### C#
```c#
public class ComboBoxValueConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, string language)
    {
        if (string.IsNullOrEmpty(value.ToString()))
            value = "Select a Value";
        return value;
    }

    public object ConvertBack(object value, Type targetType, object parameter, string language)
    {
        throw new NotImplementedException();
    }
}
```

![Showing the defualt display text in the Reports To GridComboBoxColumn](DisplayTextInReportToColumn.png)

## Requirements to run the demo
 Visual Studio 2015 and above versions