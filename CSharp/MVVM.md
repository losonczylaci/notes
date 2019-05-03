[TOC]

# Other resources

[Josh Smith's blog](https://joshsmithonwpf.wordpress.com/about/) - suggested by Steven Cleary


# Tim Corey

## MVVM using Caliburn Mirco 
[Youtube video](https://www.youtube.com/watch?v=laPFq3Fhs8k) - WPF in C# with MVVM using Caliburn Micro

**This Caliburn Mirco is a POS, it hardwires your properties and UI elements based on naming convention. It is really easy to get lost and codereview if you have no idea how it works**


* in the `App.xaml` the startupUri should be deleted and `Bootstarppe` should be referenced

* Naming convention of `Models`, `ViewModels` and `Views` are very important, because Caliburn contexts your view and viewmodel based on naming convetion

  e.g. `ShellViewModel` and `ShellView`

* ViewModel is derived from `Screen` class, as Tim said there are plenty of other base classe for this purpose within Caliburn, check them out [here](https://caliburnmicro.com/documentation/configuration).