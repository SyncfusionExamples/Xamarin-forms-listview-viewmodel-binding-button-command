# Binding button command in ListView with MVVM

The contents loaded in the [ItemTemplate](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.SfListView~ItemTemplate.html) can be bound from the view model using their commands or gestures, where you can customize the loaded content or any other action code needed in the call back. You will get the BindingContext of ListViewItem as the parameter in execution when defining the command button.

You can also get the reference of element bound as parameter by using command parameter of loaded elements.

```
<syncfusion:SfListView x:Name="listView" AutoFitMode="Height"
                SelectedItem="{Binding SelectedItem}"                      
                ItemsSource="{Binding BookInfoCollection}">
    <syncfusion:SfListView.ItemTemplate>
        <DataTemplate>
            <Frame HasShadow="True" Margin="5,5,5,5" >
                <Grid Padding="5">
                    <Grid.RowDefinitions>
                        <RowDefinition Height="*" />
                        <RowDefinition Height="2*" />
                    </Grid.RowDefinitions>
                    <Button x:Name="bookName" Text="{Binding BookName}" Command="{Binding Path=BindingContext.BackgroundColorCommand, Source={x:Reference listView}}" CommandParameter="{x:Reference bookName}}" BackgroundColor="Transparent" FontAttributes="Bold" FontSize="19"/>
                    <Label Grid.Row="1" Text="{Binding BookDescription}" FontSize="15" />
                </Grid>
            </Frame>
        </DataTemplate>
    </syncfusion:SfListView.ItemTemplate>
</syncfusion:SfListView>
```
```
public class BookInfoRepository : INotifyPropertyChanged
{
    private Command backgroundColorCommand;

    public Command BackgroundColorCommand
    {
        get { return backgroundColorCommand; }
        protected set { backgroundColorCommand = value; }
    }

    public BookInfoRepository()
    {
        backgroundColorCommand = new Command(OnButtonTapped);
    }

    ///<summary>
    ///To display tapped item content
    ///</summary>
    public void OnButtonTapped(object obj)
    {
        var firstButton = obj as Button;
        firstButton.BackgroundColor = Color.AliceBlue;            
    }
}
```
To know more about MVVM in ListView, please refer our documentation [here](https://help.syncfusion.com/xamarin/sflistview/mvvm).
