Reliable web applications require robust testing, and automation plays a key role in achieving efficiency. However, identifying and interacting with web elements can be challenging without proper element locators. This article explores the importance of well-structured element IDs and how they can simplify and enhance web test automation.

## General

Custom attributes could be added to all elements that can be used in test automation. That means all interactable elements (buttons, input fields, checkboxes), but also non-interactable elements which can contain information that is checked. 

### Naming

Because of consistency reasons, attribute names should be the same across all pages and all projects: **data-testid**. 

The value of the attribute should be unique for different elements, but there are exceptions. Also, specific elements such as buttons should have an intuitive prefix or suffix.

*Example:* 

- buttons:
<span style="display:block; border: 1px solid #e0e0e0; margin-top:15px; margin-bottom:15px; margin-left:auto; margin-right:auto; width:80%;">![Button Naming Example](/img/test_automation/web/TA_WEB_Buttons.png)</span>

- Elements added dynamically should have the same attribute value. For example, rows inside dynamically populated table:
<span style="display:block; border: 1px solid #e0e0e0; margin-top:15px; margin-bottom:15px; margin-left:auto; margin-right:auto; width:80%;">![Dynamic Element Naming Example](/img/test_automation/web/TA_WEB_Dynamic.png)</span>

- Elements inside reused components should have general attribute values that could apply to any page, but the component itself should be uniquely located:
<span style="display:block; border: 1px solid #e0e0e0; margin-top:15px; margin-bottom:15px; margin-left:auto; margin-right:auto; width:80%;">![Components Example](/img/test_automation/web/TA_WEB_Components.png)</span>

The attribute used to locate elements should be used only for test automation purposes, and potential changes in the page DOM should not affect the attribute. If the element that is located changes (for example `span` is replaced with `div`), the data-test-id attribute should be assigned to a new element.
