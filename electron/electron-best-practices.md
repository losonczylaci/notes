# Electron best practices

[video](https://www.youtube.com/watch?v=kN1Czs0m1SU) - Build an Electron App in Under 60 Minutes

> Content
>
> * Shopping list functionality 
> * a little styling 
> * deploying application

## Menus

Shortcut could be created by specifying the `accelerator` attribute of the menu item _i.e. `Ctrl+Q` \(Win and Linux\) or `Command+Q` \(Mac\)_

> For multi platfrom purpose it recommented to check the current OS
>
> ```javascript
> process.platfrom == 'darwin' ? 'Command+Q' : 'Ctrl+Q'
> ```

## MISC

* set a window to null after closing the free up the memory area
* update main window `closed` event by invoking the

  ```javascript
  app.quit()
  ```

* disclude developer tools if the sw is a production code

  ```javascript
  if ( process.env.NODE_ENV !== 'production')
  ```

* `ipcRenderer` very important to communicate between the app and the actual html view For a complete example of how to communicate between the the 'server' and the view check this video [youtube](https://youtu.be/kN1Czs0m1SU?t=1881)

