---
title: 'Using ReactiveUI with WPF in .NET 6: Best Practices and Code Examples'
subtitle: ReactiveUI is a powerful library that allows you to use reactive programming techniques within WPF applications.

# Summary for listings and search engines
summary: ReactiveUI is a powerful library that allows you to use reactive programming techniques within WPF applications. In this blog post, we'll explore how to use ReactiveUI with WPF in .NET 6, highlighting best practices and including code examples to help you get started.

# Link this post with a project
projects: []

# Date published
date: '2023-05-10T12:00:00Z'

# Date updated
lastmod: '2023-05-10T12:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
#image:
#  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
#  focal_point: ''
#  placement: 2
#  preview_only: false

authors:
  - admin

tags:
  - ReactiveUI
  - NET
  - NET6

categories:
  - ReactiveUI
  - NET
---

ReactiveUI is a powerful library that allows you to use reactive programming techniques within WPF applications. In this blog post, we'll explore how to use ReactiveUI with WPF in .NET 6, highlighting best practices and including code examples to help you get started.

## **Setting up the project**

First, let's create a new WPF application in Visual Studio, targeting .NET 6. Once the project is created, you'll need to install the necessary NuGet packages:

- `ReactiveUI.WPF` for WPF-specific functionality
- `NuGet.Protocol` for interacting with NuGet repositories in our example application

You can install these packages using the following commands:

```bash
Install-Package ReactiveUI.WPF
Install-Package NuGet.Protocol
```

[reactiveui.net](https://www.reactiveui.net/docs/getting-started/compelling-example)

## **Implementing the ViewModel**

When using ReactiveUI with the MVVM pattern, the ViewModel should inherit from `ReactiveObject`, which is the base class for all view models in ReactiveUI. This provides support for reactive properties and commands.

In your ViewModel, you can use the `WhenAnyValue` extension method to track changes of properties and perform validation on multiple properties. For example:
```csharp
this.WhenAnyValue(x => x.Username, x => x.Password,
    (username, password) => !string.IsNullOrWhiteSpace(username) && !string.IsNullOrWhiteSpace(password))
    .ToProperty(this, x => x.CanLogin, out _canLogin);
```
[medium.com](https://medium.com/@kondas/wpf-reactive-ui-firsts-steps-f8692c6901bb)

## **Creating the View**

To create a view that works with ReactiveUI, you can derive your view class from `ReactiveWindow<TViewModel>` or implement the `IViewFor` interface by hand if there isn't a suitable reactive base class available. This allows you to use the `WhenActivated` extension method for handling view and ViewModel activation and deactivation.

In the view, you can use ReactiveUI bindings to bind your ViewModel properties to view controls. Reactive bindings have some advantages over XAML-based bindings, such as generating compile  errors for property name changes instead of runtime errors.

Here's an example of how to create a view with ReactiveUI bindings:
```csharp
public partial class MainWindow : ReactiveWindow<AppViewModel>
{
    public MainWindow()
    {
        InitializeComponent();
        ViewModel = new AppViewModel();

        this.WhenActivated(disposableRegistration =>
        {
            this.OneWayBind(ViewModel,
                viewModel => viewModel.IsAvailable,
                view => view.searchResultsListBox.Visibility)
                .DisposeWith(disposableRegistration);

            this.OneWayBind(ViewModel,
                viewModel => viewModel.SearchResults,
                view => view.searchResultsListBox.ItemsSource)
                .DisposeWith(disposableRegistration);

            this.Bind(ViewModel,
                viewModel => viewModel.SearchTerm,
                view => view.searchTextBox.Text)
                .DisposeWith(disposableRegistration);
        });
    }
}
```
[reactiveui.net](https://www.reactiveui.net/docs/getting-started/compelling-example)

## **Best Practices**

When working with ReactiveUI, consider the following best practices:

- Use `WhenAny` for tracking changes of a single property and `WhenAnyValues` for multiple properties [medium.com](https://medium.com/@kondas/wpf-reactive-ui-firsts-steps-f8692c6901bb)
- Use `ReactiveCommand.CreateAsyncTask` and other `Create` functions for hooking tasks and performing result validation. Business logic and UI operations should be performed in the `Subscribe` method [medium.com](https://medium.com/@kondas/wpf-reactive-ui-firsts-steps-f8692c6901bb)
- When updating the UI from an observable (commands, events, etc.), use the `ObserveOn` method with `RxApp.MainThreadScheduler` to ensure UI updates are performed on the main thread: `ObserveOn(RxApp.MainThreadScheduler).Subscribe(...)` [medium.com](https://medium.com/@kondas/wpf-reactive-ui-firsts-steps-f8692c6901bb)
- If the solution doesn't look simple, you might be overthinking it or taking the wrong approach. Consider using observables or reevaluating
your solution [medium.com](https://medium.com/@kondas/wpf-reactive-ui-firsts-steps-f8692c6901bb)

## **Conclusion**

ReactiveUI provides a powerful way to implement reactive programming techniques in WPF applications, making it easier to create responsive and maintainable UIs. By following the best practices and using the code examples provided, you can start leveraging ReactiveUI in your WPF projects and take advantage of its many benefits.
