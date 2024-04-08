**Chapters:**

- [General](#general)
- [Android](#android)
	- [XML architecture](#xml-architecture)
	- [Compose architecture](#compose-architecture)
- [iOS](#ios)

## General

**For elements that don't have an ID, the developer should by default add IDs when working on a feature/screen** (e.g., buttons, input fields, list containers and items, titles, etc.). Additionally, if needed, the tester will make a list of elements with missing IDs so that they can be added for test automation purposes. If the tester makes a list with proposed IDs, the developer can accept the proposed one if it makes sense or discuss with the tester to name it differently.

While implementing IDs, the developer should sync with the responsible tester who will be doing the automated tests for IDs and implementation limitations. There shouldn’t be any compromises to the quality of features and usability when implementing these IDs.

### Naming

The IDs added to elements should be **unique** (most importantly - be unique on a specific screen). For that purpose, **prefixes and/or suffixes** can be used to define the ID of the component more precisely. That will be especially helpful in the case when the component consists of other sub-components which will also have IDs added to them.

*Example:* 

<span style="display:block; border: 1px solid #e0e0e0; margin-top:15px; margin-bottom:15px; margin-left:auto; margin-right:auto; width:80%;">![Android Naming Example](/img/test_automation/TA_Naming.png)</span>

Developers can follow naming conventions for their respective platform (camelCase, snake_case, or other).

## Android

### XML architecture

#### Static elements

For static elements such as buttons, titles and others that are not dynamically added Android should use **resource ID**. This is already present on a lot of views and automated tests can make use of that.
 
*Example:*

`fragment_my_profile.xml` has the profile name of the currently logged-in user. Even though the text that is displayed can be different, the ID will always be the same for that text.

<span style="display:block; border: 1px solid #e0e0e0; margin-top:15px; margin-bottom:15px; margin-left:auto; margin-right:auto; width:100%;">![Android Static Element Example](/img/test_automation/TA_Android_Static.png)</span>

#### Dynamically added elements

Dynamically added elements can be split into 2 categories. Ones that are known in advance and others that are unknown.

##### Known in advance
For the ones that are known in advance, they should be set in ids.xml file as item of type="id". After that, they can be programmatically set to the ID of an element that they represent.

*Example:*

`fragment_select_appliance_category.xml` contains `list_item_appliance_category.xml` as elements of a list. Since categories are known in advance they can be set up in `ids.xml` and added programmatically to the list item.

<span style="display:block; border: 1px solid #e0e0e0; margin-top:15px; margin-bottom:15px; margin-left:auto; margin-right:auto; width:100%;">![Android Dynamic Element Example](/img/test_automation/TA_Android_Dynamic.png)</span>

##### Unknown in advance

For list items that are not known in advance, the developer should implement an ID to the list container. After that, the testers should be able to get those elements as children of the container. Also, in case of adding IDs to individual list items that are not known in advance, it is alright if the same ID is implemented to them because the automation framework can locate such elements by combining the ID and text of the element.

NOTE: The `contentDescription` attribute should not be influenced by test automation since that attribute is used for the text-to-speech accessibility function. Such attributes will be defined on the accessibility-level implementation. If the tester needs to find an element by its text, the test automation framework can easily find an element by the displayed text, without the need to use `contentDescription`.

### Compose architecture

By default, composables are accessible from [UiAutomator](https://developer.android.com/training/testing/other-components/ui-automator) only by their convenient descriptors (displayed text, content description, etc.). 

In order to add IDs and access composables by resource ID using UiAutomator, the developer first needs to enable the semantic property `testTagAsResourceId` for the particular composables subtree. This will map `testTag` properties to resource IDs. Enabling it at the top-level composable will ensure all of the nested composables with `Modifier.testTag(tag)` are accessible from UiAutomator and allow the automation framework to find the UI components from a given test tag.

*Example:*

<span style="display:block; border: 1px solid #e0e0e0; margin-top:15px; margin-bottom:15px; margin-left:auto; margin-right:auto; width:70%;">![Android Compose Example](/img/test_automation/TA_Android_Compose.png)</span>

## iOS

### Accessibility Identifier

For UI testing purposes Apple provides us with a so-called accessibilityIdentifier. It is meant to "be used to uniquely identify a UI element in the scripts we write using the UI Automation interfaces". Accessibility identifiers aren't accessed by e.g. VoiceOver. They are part of the `UIAccessibilityIdentification` protocol, which consists of methods that associate a **unique identifier** with elements in a user interface. The only strict requirement for adhering to this protocol is defining the `accessibilityIdentifier` property.

`UIAccessibilityIdentification: var accessibilityIdentifier: String? { get set }`

The mobile developer needs to set accessibilityIdentifiers on elements that are being inspected as a part of test automation (e.g., buttons, input fields, list containers and items, titles, etc.). An accessibility identifier can be set using storyboards or programmatically. In our app, we should set it programmatically to have more readable code and to make changes easier if some identifier needs to be updated.

For list items that are not known in advance, the developer should implement an ID to the list container. After that, the testers should be able to get those elements as children of the container. Also, in case of adding IDs to individual list items that are not known in advance, it is alright if the same ID is implemented to them because the automation framework can locate such elements by combining the ID and text of the element.

### Testing

Implementation can be tested using [Accessibility Inspector](https://developer.apple.com/videos/play/wwdc2019/257/), and checking `Basic → Identifier`.

<span style="display:block; border: 1px solid #e0e0e0; margin-top:15px; margin-bottom:15px; margin-left:auto; margin-right:auto; width:80%;">![iOS Accessibility Inspector](/img/test_automation/TA_iOS_Accessibility_Inspector.png)</span>
