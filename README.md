# pyqt-hotkey-picker
A simple and customizable hotkey picker widget for PyQt5

![pyqt-hotkey-picker](https://github.com/niklashenning/pyqt-hotkey-picker/assets/58544929/4b5104ed-0848-4346-a81c-f61bdd40dde0)

## Installation
Download the **hotkey_picker.py** file from the **src** folder and add it to your project

## Usage
Import the `HotkeyPicker` class and add it to your window like any other PyQt Widget:
```python
from PyQt5.QtWidgets import QMainWindow
from PyQt5.QtCore import Qt
from hotkey_picker import HotkeyPicker


class Window(QMainWindow):
    def __init__(self):
        super().__init__(parent=None)

        # Add hotkey picker with default settings
        demo_hotkey_picker = HotkeyPicker(self)
        # Connect change event
        demo_hotkey_picker.hotkeyChanged.connect(self.hotkey_changed)
    
    # Called every time the picked hotkey changes
    def hotkey_changed(self, key, key_name):
        print([key, key_name])
```
Use the `getHotkey()` and `getHotkeyString()` methods to get the key code and name of the selected hotkey:

```python
# Returns int with key code if a hotkey is selected, otherwise 0
key_code = demo_hotkey_picker.getHotkey()  # e.g. 65 (which is the same as Qt.Key_A)

# Returns string with key name if a hotkey is selected, otherwise empty string
key_name = demo_hotkey_picker.getHotkeyString()  # e.g. 'Shift'
```

Use the `setHotkey()` method to set the selected hotkey and the `reset()` method to reset the hotkey picker to the default state with no selected hotkey:

```python
demo_hotkey_picker.setHotkey(Qt.Key_A)  # could also directly pass int (e.g. 65)

demo_hotkey_picker.reset()
```

You can also use the static `keyCodeToString()` method to get the name of a key:

```python
key_name_1 = HotkeyPicker.keyCodeToString(Qt.Key_A)  # 'A'
key_name_2 = HotkeyPicker.keyCodeToString(16777268)  # 'F5'
```

More in-depth examples can be found in the [examples](examples) folder

## Customization
* **Changing the cancel key used to exit the hotkey selection:**

  ```python
  # On initialization
  demo_hotkey_picker = HotkeyPicker(self, cancel_key=Qt.Key_Return)
  
  # Or using the setter
  demo_hotkey_picker.setCancelKey(Qt.Key_Return)  # Default value: Qt.Key_Escape
  ```
  
* **Changing the default text of the hotkey picker:**

   ```python
   # On initialization
   demo_hotkey_picker = HotkeyPicker(self, default_text='Not selected..')
  
   # Or using the setter
   demo_hotkey_picker.setDefaultText('Not selected..')  # Default value: 'None'
   ```

* **Changing the text of the hotkey picker that is shown when waiting for a key press:**

   ```python
   # On initialization
   demo_hotkey_picker = HotkeyPicker(self, selecting_text='Selecting..')
  
   # Or using the setter
   demo_hotkey_picker.setSelectingText('Selecting..')  # Default value: '..'
   ```

* **Only allowing specific keys to be selected:**

   ```python
   # List of allowed keys (no other key can be selected)
   keys = [Qt.Key_F1, Qt.Key_F2, Qt.Key_F3, Qt.Key_F4, Qt.Key_F5, Qt.Key_F6,
           Qt.Key_F7, Qt.Key_F8, Qt.Key_F9, Qt.Key_F10, Qt.Key_F11, Qt.Key_F12]
   
   # On initialization 
   demo_hotkey_picker = HotkeyPicker(self, filter_keys=True, allowed_keys=keys)
   
   # Or using the setter
   demo_hotkey_picker.filterKeys(True)
   demo_hotkey_picker.setAllowedKeys(keys)
   ```

* **Not allowing specific keys to be selected:**

   ```python
   # List of forbidden keys (every other key can be selected)
   keys = [Qt.Key_F1, Qt.Key_F2, Qt.Key_F3, Qt.Key_F4, Qt.Key_F5]
   
   # On initialization 
   demo_hotkey_picker = HotkeyPicker(self, filter_keys=True, forbidden_keys=keys)
   
   # Or using the setter
   demo_hotkey_picker.filterKeys(True)
   demo_hotkey_picker.setForbiddenKeys(keys)
   ```
  **Note**: Only one of these filter options can be set per hotkey picker, meaning you can either specify the exact keys you want to allow or specify the exact keys you want to forbid.

## License
This software is licensed under the [MIT license](LICENSE).
