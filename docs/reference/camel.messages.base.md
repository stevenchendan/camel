<a id="camel.messages.base"></a>

<a id="camel.messages.base.BaseMessage"></a>

## BaseMessage

```python
class BaseMessage:
```

Base class for message objects used in CAMEL chat system.

**Parameters:**

- **role_name** (str): The name of the user or assistant role.
- **role_type** (RoleType): The type of role, either :obj:`RoleType. ASSISTANT` or :obj:`RoleType.USER`.
- **meta_dict** (Optional[Dict[str, Any]]): Additional metadata dictionary for the message.
- **content** (str): The content of the message.
- **video_bytes** (Optional[bytes]): Optional bytes of a video associated with the message. (default: :obj:`None`)
- **image_list** (Optional[List[Image.Image]]): Optional list of PIL Image objects associated with the message. (default: :obj:`None`)
- **image_detail** (`Literal["auto", "low", "high"]`): Detail level of the images associated with the message. (default: :obj:`auto`)
- **video_detail** (`Literal["auto", "low", "high"]`): Detail level of the videos associated with the message. (default: :obj:`auto`)
- **parsed**: Optional[Union[Type[BaseModel], dict]]: Optional object which is parsed from the content. (default: :obj:`None`)

<a id="camel.messages.base.BaseMessage.make_user_message"></a>

### make_user_message

```python
def make_user_message(
    cls,
    role_name: str,
    content: str,
    meta_dict: Optional[Dict[str, str]] = None,
    video_bytes: Optional[bytes] = None,
    image_list: Optional[List[Image.Image]] = None,
    image_detail: Union[OpenAIVisionDetailType, str] = OpenAIVisionDetailType.AUTO,
    video_detail: Union[OpenAIVisionDetailType, str] = OpenAIVisionDetailType.LOW
):
```

Create a new user message.

**Parameters:**

- **role_name** (str): The name of the user role.
- **content** (str): The content of the message.
- **meta_dict** (Optional[Dict[str, str]]): Additional metadata dictionary for the message.
- **video_bytes** (Optional[bytes]): Optional bytes of a video associated with the message.
- **image_list** (Optional[List[Image.Image]]): Optional list of PIL Image objects associated with the message.
- **image_detail** (Union[OpenAIVisionDetailType, str]): Detail level of the images associated with the message.
- **video_detail** (Union[OpenAIVisionDetailType, str]): Detail level of the videos associated with the message.

**Returns:**

  BaseMessage: The new user message.

<a id="camel.messages.base.BaseMessage.make_assistant_message"></a>

### make_assistant_message

```python
def make_assistant_message(
    cls,
    role_name: str,
    content: str,
    meta_dict: Optional[Dict[str, str]] = None,
    video_bytes: Optional[bytes] = None,
    image_list: Optional[List[Image.Image]] = None,
    image_detail: Union[OpenAIVisionDetailType, str] = OpenAIVisionDetailType.AUTO,
    video_detail: Union[OpenAIVisionDetailType, str] = OpenAIVisionDetailType.LOW
):
```

Create a new assistant message.

**Parameters:**

- **role_name** (str): The name of the assistant role.
- **content** (str): The content of the message.
- **meta_dict** (Optional[Dict[str, str]]): Additional metadata dictionary for the message.
- **video_bytes** (Optional[bytes]): Optional bytes of a video associated with the message.
- **image_list** (Optional[List[Image.Image]]): Optional list of PIL Image objects associated with the message.
- **image_detail** (Union[OpenAIVisionDetailType, str]): Detail level of the images associated with the message.
- **video_detail** (Union[OpenAIVisionDetailType, str]): Detail level of the videos associated with the message.

**Returns:**

  BaseMessage: The new assistant message.

<a id="camel.messages.base.BaseMessage.create_new_instance"></a>

### create_new_instance

```python
def create_new_instance(self, content: str):
```

Create a new instance of the :obj:`BaseMessage` with updated
content.

**Parameters:**

- **content** (str): The new content value.

**Returns:**

  BaseMessage: The new instance of :obj:`BaseMessage`.

<a id="camel.messages.base.BaseMessage.__add__"></a>

### __add__

```python
def __add__(self, other: Any):
```

Addition operator override for :obj:`BaseMessage`.

**Parameters:**

- **other** (Any): The value to be added with.

**Returns:**

  Union[BaseMessage, Any]: The result of the addition.

<a id="camel.messages.base.BaseMessage.__mul__"></a>

### __mul__

```python
def __mul__(self, other: Any):
```

Multiplication operator override for :obj:`BaseMessage`.

**Parameters:**

- **other** (Any): The value to be multiplied with.

**Returns:**

  Union[BaseMessage, Any]: The result of the multiplication.

<a id="camel.messages.base.BaseMessage.__len__"></a>

### __len__

```python
def __len__(self):
```

**Returns:**

  int: The length of the content.

<a id="camel.messages.base.BaseMessage.__contains__"></a>

### __contains__

```python
def __contains__(self, item: str):
```

Contains operator override for :obj:`BaseMessage`.

**Parameters:**

- **item** (str): The item to check for containment.

**Returns:**

  bool: :obj:`True` if the item is contained in the content,
:obj:`False` otherwise.

<a id="camel.messages.base.BaseMessage.extract_text_and_code_prompts"></a>

### extract_text_and_code_prompts

```python
def extract_text_and_code_prompts(self):
```

**Returns:**

  Tuple[List[TextPrompt], List[CodePrompt]]: A tuple containing a
list of text prompts and a list of code prompts extracted
from the content.

<a id="camel.messages.base.BaseMessage.from_sharegpt"></a>

### from_sharegpt

```python
def from_sharegpt(
    cls,
    message: ShareGPTMessage,
    function_format: Optional[FunctionCallFormatter[Any, Any]] = None,
    role_mapping = None
):
```

Convert ShareGPT message to BaseMessage or FunctionCallingMessage.
Note tool calls and responses have an 'assistant' role in CAMEL

**Parameters:**

- **message** (ShareGPTMessage): ShareGPT message to convert.
- **function_format** (FunctionCallFormatter, optional): Function call formatter to use. (default: :obj:`HermesFunctionFormatter()`.
- **role_mapping** (Dict[str, List[str, RoleType]], optional): Role mapping to use. Defaults to a CAMEL specific mapping.

**Returns:**

  BaseMessage: Converted message.

<a id="camel.messages.base.BaseMessage.to_sharegpt"></a>

### to_sharegpt

```python
def to_sharegpt(self, function_format: Optional[FunctionCallFormatter] = None):
```

Convert BaseMessage to ShareGPT message

**Parameters:**

- **function_format** (FunctionCallFormatter): Function call formatter to use. Defaults to Hermes.

<a id="camel.messages.base.BaseMessage.to_openai_message"></a>

### to_openai_message

```python
def to_openai_message(self, role_at_backend: OpenAIBackendRole):
```

Converts the message to an :obj:`OpenAIMessage` object.

**Parameters:**

- **role_at_backend** (OpenAIBackendRole): The role of the message in OpenAI chat system.

**Returns:**

  OpenAIMessage: The converted :obj:`OpenAIMessage` object.

<a id="camel.messages.base.BaseMessage.to_openai_system_message"></a>

### to_openai_system_message

```python
def to_openai_system_message(self):
```

**Returns:**

  OpenAISystemMessage: The converted :obj:`OpenAISystemMessage`
object.

<a id="camel.messages.base.BaseMessage.to_openai_user_message"></a>

### to_openai_user_message

```python
def to_openai_user_message(self):
```

**Returns:**

  OpenAIUserMessage: The converted :obj:`OpenAIUserMessage` object.

<a id="camel.messages.base.BaseMessage.to_openai_assistant_message"></a>

### to_openai_assistant_message

```python
def to_openai_assistant_message(self):
```

**Returns:**

  OpenAIAssistantMessage: The converted :obj:`OpenAIAssistantMessage`
object.

<a id="camel.messages.base.BaseMessage.to_dict"></a>

### to_dict

```python
def to_dict(self):
```

**Returns:**

  dict: The converted dictionary.
