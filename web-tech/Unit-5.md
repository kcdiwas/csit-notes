### Unit V: AJAX and XML (7 Hours)
This unit has two big parts: AJAX (which helps web pages update without refreshing) and XML (a way to store and organize data). It’s a 7-hour chunk in your syllabus, split between lectures and lab work. Here’s what you need to know:

---

#### 5.1 Basics of AJAX
AJAX stands for **Asynchronous JavaScript and XML**. It’s a technique that lets your web page talk to a server in the background and update parts of the page without reloading the whole thing. Think of it like sending a quick text to a friend and getting a reply without leaving the room.

- **How it works**: You use JavaScript (specifically something called `XMLHttpRequest`) to send a request to the server. The server sends back data (could be text, JSON, or XML), and you update the page with it.
- **Why it’s cool**: No full page refresh! It’s fast and feels smooth—like when you see new comments load on a post without clicking anything.

**Example**: Imagine a weather app. You type in a city name, and the temperature updates instantly without the page reloading. That’s AJAX at work.

```javascript
// Simple AJAX example
let xhr = new XMLHttpRequest();
xhr.open("GET", "weather.php?city=London", true); // Sending a request to a PHP file
xhr.onreadystatechange = function() {
    if (xhr.readyState == 4 && xhr.status == 200) {
        document.getElementById("result").innerHTML = xhr.responseText; // Update the page
    }
};
xhr.send();
```
Here, `weather.php` might send back something like "25°C," and it shows up in a `<div id="result">` on your page.

---

#### 5.2 Introduction to XML and Its Application
XML stands for **Extensible Markup Language**. It’s like HTML’s cousin but stricter and more about storing data than displaying it. You create your own tags to describe the data, making it super flexible.

- **What it does**: It’s a way to structure data so both humans and computers can read it. It’s used a lot in web services, like sending data between a server and a client.
- **Application**: Think of an online store sending product details (name, price, stock) to an app—that could be in XML.

**Example**:
```xml
<product>
    <name>Laptop</name>
    <price>800</price>
    <stock>10</stock>
</product>
```
This is simple and readable, right? The tags tell you exactly what each piece of data is.

---

#### 5.3 Syntax Rules for Creating XML Document
XML has some rules to keep it neat and tidy:
1. **One root element**: Everything must be inside a single main tag (like `<root>`).
2. **Tags must close**: `<name>Laptop</name>` (no leaving it open like `<name>`).
3. **Case-sensitive**: `<Name>` and `<name>` are different.
4. **Proper nesting**: `<a><b>Text</b></a>` (no overlapping like `<a><b></a></b>`).
5. **Attributes in quotes**: `<item id="1">` (not `<item id=1>`).

**Example**:
```xml
<store>
    <item id="1">
        <name>Book</name>
        <price>15</price>
    </item>
</store>
```
This follows all the rules—root tag is `<store>`, everything’s closed, and the attribute `id` is quoted.

---

#### 5.4 XML Elements; XML Attributes; XML Tree
- **Elements**: The building blocks of XML, like `<name>` or `<price>`. They can hold data or other elements.
- **Attributes**: Extra info inside a tag, like `id="1"` in `<item id="1">`.
- **XML Tree**: Think of XML as a family tree. The root is the parent, and nested tags are children.

**Example**:
```xml
<school>
    <student id="101">
        <name>John</name>
        <grade>A</grade>
    </student>
</school>
```
- Root: `<school>`
- Child: `<student>` (with attribute `id="101"`)
- Grandchildren: `<name>` and `<grade>`

---

#### 5.5 XML Namespace
Namespaces prevent confusion when two XML files use the same tag names but mean different things. You add a prefix and a URL to make tags unique.

**Example**:
```xml
<school xmlns:stu="http://example.com/students">
    <stu:name>John</stu:name>
    <stu:grade>A</stu:grade>
</school>
```
Here, `stu:` is the prefix, and the URL (even if it’s fake) identifies where these tags come from.


<details>
  <summary>Read More details about XML Namespace</summary>


#### What’s an XML Namespace, Really?
An XML Namespace is like a way to give your tags a unique identity so they don’t get mixed up with other tags that might have the same name. Imagine you’re at a party with two people named “John”—you’d need a last name (like “John Smith” vs. “John Doe”) to tell them apart. Namespaces do that for XML tags.

- **Why it’s needed**: XML is flexible—you make your own tags. But if two systems (say, a school and a store) both use `<name>`, how do you know if it’s a student’s name or a product’s name? Namespaces solve this by adding a “family name” (a prefix) tied to a unique identifier (usually a URL).
- **How it works**: You attach a prefix (like `stu:` or `prod:`) to tags and link it to a namespace URI (a web address, real or fake). The URI doesn’t have to point to a real page—it’s just a unique label.

---

#### Key Pieces of a Namespace
1. **Prefix**: A short label you stick in front of tags (e.g., `stu:` in `stu:name`). It’s like a nickname for the namespace.
2. **Namespace URI**: A unique string (usually a URL) that defines the namespace (e.g., `http://example.com/students`). Think of it as the “official ID.”
3. **Declaration**: You tell XML about the namespace using `xmlns` (XML Namespace attribute) in a tag.

---

#### How to Declare a Namespace
You declare a namespace in an XML tag (usually the root) with `xmlns:prefix="URI"`. Once declared, you use the prefix on tags to show they belong to that namespace.

**Basic Example**:
```xml
<school xmlns:stu="http://example.com/students">
    <stu:name>John</stu:name>
    <stu:grade>A</stu:grade>
</school>
```
- **Breakdown**:
  - `xmlns:stu="http://example.com/students"`: Declares the namespace. `stu:` is the prefix, and the URL is the URI.
  - `stu:name`: The `<name>` tag belongs to the `http://example.com/students` namespace.
  - Without the prefix, `<name>` would be “unqualified” (no namespace).

---

#### Why Bother with Namespaces?
Here’s where it gets practical. Say you’re combining two XML files:
1. A school system:
```xml
<record>
    <name>John</name>
    <grade>A</grade>
</record>
```
2. A store system:
```xml
<record>
    <name>Laptop</name>
    <price>800</price>
</record>
```
Now, mix them in one file:
```xml
<database>
    <record>
        <name>John</name>
        <grade>A</grade>
    </record>
    <record>
        <name>Laptop</name>
        <price>800</price>
    </record>
</database>
```
- **Problem**: Which `<name>` is which? Is it a student or a product? Confusion!

**Fix with Namespaces**:
```xml
<database xmlns:stu="http://example.com/students" xmlns:prod="http://example.com/products">
    <stu:record>
        <stu:name>John</stu:name>
        <stu:grade>A</stu:grade>
    </stu:record>
    <prod:record>
        <prod:name>Laptop</prod:name>
        <prod:price>800</prod:price>
    </prod:record>
</database>
```
- **Result**: `stu:name` (student) and `prod:name` (product) are clearly different. No mix-up!

---

#### Default Namespace (No Prefix)
You can set a namespace without a prefix using just `xmlns="URI"`. All tags without a prefix in that section belong to it.

**Example**:
```xml
<school xmlns="http://example.com/students">
    <name>John</name>
    <grade>A</grade>
</school>
```
- **Means**: `<name>` and `<grade>` belong to `http://example.com/students`. No `stu:` needed.
- **Mixing with Prefix**:
```xml
<root xmlns="http://example.com/default" xmlns:stu="http://example.com/students">
    <name>Default Name</name>
    <stu:name>John</stu:name>
</root>
```
- `<name>`: Uses the default namespace.
- `<stu:name>`: Uses the `stu:` namespace.

---

#### Scope of Namespaces
- A namespace applies to the tag it’s declared in and all its children—unless overridden.
- You can declare a new namespace lower down to change it.

**Example**:
```xml
<root xmlns:stu="http://example.com/students">
    <stu:name>John</stu:name>
    <class xmlns:stu="http://example.com/classes">
        <stu:name>Web Tech</stu:name>
    </class>
</root>
```
- **Outside `<class>`**: `stu:` means students.
- **Inside `<class>`**: `stu:` means classes (overrides the parent).

---

#### Real-World Use
- **Web Services**: SOAP (an old web protocol) uses namespaces to separate message parts (e.g., `soap:envelope`).
- **XHTML**: Combines HTML with XML namespaces (e.g., `xmlns="http://www.w3.org/1999/xhtml"`).
- **Mixing Data**: Like our school/store example—namespaces keep everything clear.

**SOAP Example**:
```xml
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <m:GetPrice xmlns:m="http://example.com/store">
            <m:Item>Laptop</m:Item>
        </m:GetPrice>
    </soap:Body>
</soap:Envelope>
```
- `soap:` and `m:` keep the tags distinct.

---

#### Common Exam Points
- **Syntax**: Know `xmlns:prefix="URI"` and how to use prefixes.
- **Purpose**: Explain avoiding tag conflicts (e.g., two `<name>` tags).
- **Default vs. Prefixed**: Understand the difference.
- **Example**: Be ready to write one—like the school/store mix.

**Practice Question**:  
“Create an XML snippet with two namespaces for a library and a bookstore, each with a `<book>` tag.”  
Answer:
```xml
<root xmlns:lib="http://example.com/library" xmlns:store="http://example.com/bookstore">
    <lib:book>
        <lib:title>Web Tech</lib:title>
    </lib:book>
    <store:book>
        <store:title>Laptop Guide</store:title>
    </store:book>
</root>
```

</details>

---
#### 5.6 XML Schema Languages: DTD and XSD
These are like rulebooks for XML to make sure it’s structured correctly.
- **DTD (Document Type Definition)**: An older, simpler way to define rules.
  ```xml
  <!DOCTYPE school [
      <!ELEMENT school (student)>
      <!ELEMENT student (name, grade)>
      <!ELEMENT name (#PCDATA)>
      <!ELEMENT grade (#PCDATA)>
  ]>
  ```
  This says a `<school>` must have a `<student>`, which has `<name>` and `<grade>`.

- **XSD (XML Schema Definition)**: More detailed and modern.
  - **Simple Types**: Like `<xs:element name="age" type="xs:integer"/>` (only numbers).
  - **Attributes**: `<xs:attribute name="id" type="xs:string"/>`.
  - **Complex Types**: Allows nesting, like a `<student>` with `<name>` and `<grade>`.

**Example XSD**:
```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="student">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="name" type="xs:string"/>
                <xs:element name="grade" type="xs:string"/>
            </xs:sequence>
            <xs:attribute name="id" type="xs:integer"/>
        </xs:complexType>
    </xs:element>
</xs:schema>
```
This defines a `<student>` with a required `id`, `<name>`, and `<grade>`.

---

<details>
  <summary style="color: red;">Read more about XML Schema Languages</summary>  
---

Both **DTD (Document Type Definition)** and **XSD (XML Schema Definition)** are ways to define the structure and rules of an XML document. They’re like blueprints for a house—telling you what rooms (elements) should be there and how they’re arranged. But they’re different in how strict and detailed they are. Let’s break them down.

#### DTD (Document Type Definition)
DTD is the older, simpler way to set rules for XML. It’s like a basic checklist—it tells you what elements and attributes are allowed, but it doesn’t get too fancy with details like data types (e.g., “this must be a number”).

- **What it does**: Defines the structure—what elements can exist, their order, and whether they’re optional or required. It can also list attributes.
- **Where it lives**: Can be inside the XML file (internal) or in a separate `.dtd` file (external).
- **Limitations**: No support for data types (e.g., can’t say “age must be an integer”), and it’s less flexible than XSD.

**Syntax Basics**:
- `<!ELEMENT>`: Defines an element and what it can contain.
- `<!ATTLIST>`: Defines attributes for an element.
- Symbols:
  - `#PCDATA`: Plain text (like names or grades).
  - `+`: One or more times.
  - `*`: Zero or more times.
  - `?`: Optional (zero or one time).

**Example (Internal DTD)**:
```xml
<?xml version="1.0"?>
<!DOCTYPE class [
    <!ELEMENT class (student+)>
    <!ELEMENT student (name, age)>
    <!ELEMENT name (#PCDATA)>
    <!ELEMENT age (#PCDATA)>
    <!ATTLIST student id CDATA #REQUIRED>
]>
<class>
    <student id="101">
        <name>John</name>
        <age>20</age>
    </student>
    <student id="102">
        <name>Mary</name>
        <age>21</age>
    </student>
</class>
```
- **Explanation**:
  - `class` is the root and must have one or more `student` elements (`student+`).
  - Each `student` has a `name` and `age`, both text (`#PCDATA`).
  - `student` must have an `id` attribute (`#REQUIRED`), and it’s just text (`CDATA`).

**External DTD Example**:
Save this as `class.dtd`:
```dtd
<!ELEMENT class (student+)>
<!ELEMENT student (name, age)>
<!ELEMENT name (#PCDATA)>
<!ELEMENT age (#PCDATA)>
<!ATTLIST student id CDATA #REQUIRED>
```
Then link it in XML:
```xml
<?xml version="1.0"?>
<!DOCTYPE class SYSTEM "class.dtd">
<class>
    <student id="101">
        <name>John</name>
        <age>20</age>
    </student>
</class>
```
- **Why use it?**: It’s simple and good for basic XML files, but it’s old-school and limited.

---

#### XSD (XML Schema Definition)
XSD is the modern, more powerful option. It’s like DTD’s upgraded version—it’s stricter, supports data types (e.g., “age must be a number”), and can handle complex structures. It’s written in XML itself, which makes it easier to read and work with.

- **What it does**: Defines elements, attributes, their order, and their data types (like string, integer, date). It’s way more detailed than DTD.
- **Why it’s better**: You can say “age must be between 0 and 100” or “email must follow a pattern.” DTD can’t do that.
- **Parts**:
  - **Simple Types**: Elements or attributes with basic data (e.g., text, numbers).
  - **Complex Types**: Elements that contain other elements or have attributes.
  - **Attributes**: Extra info for elements, with rules like “required” or “optional.”

**Syntax Basics**:
- Written in XML with a namespace (`xmlns:xs="http://www.w3.org/2001/XMLSchema"`).
- `<xs:element>`: Defines an element.
- `<xs:attribute>`: Defines an attribute.
- `<xs:complexType>`: For elements with children or attributes.
- `<xs:simpleType>`: For basic data with restrictions (e.g., min/max values).

**Example (Basic XSD)**:
```xml
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="class">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="student" maxOccurs="unbounded">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="name" type="xs:string"/>
                            <xs:element name="age" type="xs:integer"/>
                        </xs:sequence>
                        <xs:attribute name="id" type="xs:string" use="required"/>
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```
- **Explanation**:
  - `class` is the root and can have unlimited `student` elements (`maxOccurs="unbounded"`).
  - Each `student` has a `name` (string), `age` (integer), and a required `id` attribute (string).
- Matching XML:
```xml
<class>
    <student id="101">
        <name>John</name>
        <age>20</age>
    </student>
</class>
```

#### XSD Elements
**What are Elements?**  
Elements are the main tags in your XML—like `<name>`, `<age>`, or `<student>`. In XSD, you define them with `<xs:element>` to say what they’re called, what type of data they hold, and how many times they can appear.

- **Key Attributes**:
  - `name`: The element’s tag name (e.g., "student").
  - `type`: What kind of data (e.g., `xs:string`, `xs:integer`, or a custom type).
  - `minOccurs`/`maxOccurs`: How many times it can show up (e.g., `0` for optional, `unbounded` for unlimited).

**Simple Element Example**:  
```xml
<xs:element name="name" type="xs:string"/>
```
- **Means**: A `<name>` tag that holds text (e.g., `<name>John</name>`).

**In XML**:  
```xml
<name>John</name>
```

**Element with Limits**:  
```xml
<xs:element name="student" type="xs:string" minOccurs="1" maxOccurs="3"/>
```
- **Means**: Must have 1-3 `<student>` tags.
- **Valid XML**:  
```xml
<student>John</student>
<student>Mary</student>
```
- **Invalid**: None (less than 1) or 4 `<student>` tags (more than 3).

---

#### XSD Attributes
**What are Attributes?**  
Attributes are extra bits of info inside an element’s tag—like `id="101"` in `<student id="101">`. In XSD, you define them with `<xs:attribute>`.

- **Key Attributes**:
  - `name`: The attribute’s name (e.g., "id").
  - `type`: Data type (e.g., `xs:string`, `xs:integer`).
  - `use`: `required` (must be there) or `optional` (can skip it).

**Example**:  
```xml
<xs:element name="student">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="name" type="xs:string"/>
        </xs:sequence>
        <xs:attribute name="id" type="xs:integer" use="required"/>
    </xs:complexType>
</xs:element>
```
- **Means**: `<student>` has a `<name>` inside and a required `id` attribute.
- **Valid XML**:  
```xml
<student id="101">
    <name>John</name>
</student>
```
- **Invalid**: `<student><name>John</name></student>` (missing `id`).

**Optional Attribute**:  
```xml
<xs:attribute name="grade" type="xs:string" use="optional"/>
```
- **Valid XML**:  
```xml
<student id="101" grade="A"><name>John</name></student>
```
or  
```xml
<student id="101"><name>John</name></student>
```

---

#### XSD Restrictions
**What are Restrictions?**  
Restrictions let you put rules on simple types—like “age must be 0-100” or “name must be 2-50 characters.” You use `<xs:restriction>` to tighten up what’s allowed.

- **Where Used**: Inside `<xs:simpleType>` for elements or attributes.
- **Common Restrictions**:
  - `minInclusive`/`maxInclusive`: Range for numbers (includes the limits).
  - `minLength`/`maxLength`: Length for strings.
  - `pattern`: A regex to match (e.g., “must start with a letter”).

**Example (Number Range)**:  
```xml
<xs:element name="age">
    <xs:simpleType>
        <xs:restriction base="xs:integer">
            <xs:minInclusive value="0"/>
            <xs:maxInclusive value="100"/>
        </xs:restriction>
    </xs:simpleType>
</xs:element>
```
- **Means**: `<age>` must be 0-100.
- **Valid**: `<age>20</age>`
- **Invalid**: `<age>-5</age>` or `<age>150</age>`

**Example (String Length)**:  
```xml
<xs:element name="name">
    <xs:simpleType>
        <xs:restriction base="xs:string">
            <xs:minLength value="2"/>
            <xs:maxLength value="50"/>
        </xs:restriction>
    </xs:simpleType>
</xs:element>
```
- **Means**: `<name>` must be 2-50 characters.
- **Valid**: `<name>John</name>`
- **Invalid**: `<name>J</name>` (too short).

**Example (Pattern)**:  
```xml
<xs:element name="code">
    <xs:simpleType>
        <xs:restriction base="xs:string">
            <xs:pattern value="[A-Z][0-9]{3}"/>
        </xs:restriction>
    </xs:simpleType>
</xs:element>
```
- **Means**: `<code>` must be one uppercase letter + three digits (e.g., "A123").
- **Valid**: `<code>B456</code>`
- **Invalid**: `<code>abc</code>` or `<code>A12</code>`.

---

#### XSD Complex Types
**What are Complex Types?**  
Complex types are for elements that have children (other elements) or attributes—unlike simple types (just text or numbers). You use `<xs:complexType>` to define them.

- **Why Needed**: A `<student>` with `<name>` and `<age>` inside isn’t simple—it’s complex because it has structure.
- **Parts**:
  - `<xs:sequence>`: Kids must appear in order.
  - `<xs:choice>`: Pick one of the kids.
  - `<xs:all>`: Kids can be in any order (but all must appear if not optional).

**Example (Sequence)**:  
```xml
<xs:element name="student">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="name" type="xs:string"/>
            <xs:element name="age" type="xs:integer"/>
        </xs:sequence>
        <xs:attribute name="id" type="xs:string" use="required"/>
    </xs:complexType>
</xs:element>
```
- **Means**: `<student>` must have `<name>` then `<age>`, and a required `id`.
- **Valid XML**:  
```xml
<student id="101">
    <name>John</name>
    <age>20</age>
</student>
```
- **Invalid**: `<student id="101"><age>20</age><name>John</name></student>` (wrong order).

**Example (Choice)**:  
```xml
<xs:element name="contact">
    <xs:complexType>
        <xs:choice>
            <xs:element name="phone" type="xs:string"/>
            <xs:element name="email" type="xs:string"/>
        </xs:choice>
    </xs:complexType>
</xs:element>
```
- **Means**: `<contact>` has either `<phone>` or `<email>`, not both.
- **Valid**: `<contact><phone>123-456</phone></contact>`  
or `<contact><email>john@example.com</email></contact>`
- **Invalid**: `<contact><phone>123</phone><email>john</email></contact>`.

**Example (All)**:  
```xml
<xs:element name="person">
    <xs:complexType>
        <xs:all>
            <xs:element name="name" type="xs:string"/>
            <xs:element name="age" type="xs:integer"/>
        </xs:all>
    </xs:complexType>
</xs:element>
```
- **Means**: `<person>` needs both `<name>` and `<age>`, but order doesn’t matter.
- **Valid**:  
```xml
<person><name>John</name><age>20</age></person>
```
or  
```xml
<person><age>20</age><name>John</name></person>
```

**Complex with Restrictions**:  
```xml
<xs:element name="student">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="name" type="xs:string"/>
            <xs:element name="age">
                <xs:simpleType>
                    <xs:restriction base="xs:integer">
                        <xs:minInclusive value="0"/>
                        <xs:maxInclusive value="100"/>
                    </xs:restriction>
                </xs:simpleType>
            </xs:element>
        </xs:sequence>
        <xs:attribute name="id" type="xs:string" use="required"/>
    </xs:complexType>
</xs:element>
```
- **Means**: `<student>` has `<name>`, `<age>` (0-100), and a required `id`.

---

#### Putting It All Together
**Full Example**:  
```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="class">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="student" maxOccurs="unbounded">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="name">
                                <xs:simpleType>
                                    <xs:restriction base="xs:string">
                                        <xs:minLength value="2"/>
                                        <xs:maxLength value="50"/>
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:element>
                            <xs:element name="age">
                                <xs:simpleType>
                                    <xs:restriction base="xs:integer">
                                        <xs:minInclusive value="0"/>
                                        <xs:maxInclusive value="100"/>
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:element>
                        </xs:sequence>
                        <xs:attribute name="id" type="xs:string" use="required"/>
                        <xs:attribute name="grade" type="xs:string" use="optional"/>
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```
- **Valid XML**:  
```xml
<class>
    <student id="101" grade="A">
        <name>John</name>
        <age>20</age>
    </student>
    <student id="102">
        <name>Mary</name>
        <age>21</age>
    </student>
</class>
```

### DTD vs. XSD: Quick Comparison
| Feature              | DTD                          | XSD                          |
|----------------------|------------------------------|------------------------------|
| **Format**           | Not XML (own syntax)         | Written in XML              |
| **Data Types**       | No (just text with `#PCDATA`)| Yes (string, int, date, etc.)|
| **Complexity**       | Simple structures only       | Handles complex nesting     |
| **Restrictions**     | None (e.g., no min/max)      | Yes (e.g., age 0-100)       |
| **Modern Use**       | Older, less common now       | Standard for web services   |

---

### Why This Matters for Your Exam
- **DTD**: Know how to write a basic one (like the `class` example) and understand `#PCDATA`, `+`, `*`, `?`. The exam might ask you to define a simple structure.
- **XSD**: Focus on simple and complex types, and maybe a restriction (like `minInclusive`). You might need to write or explain an XSD snippet.
---

### Extra Example (Side-by-Side)
**XML**:
```xml
<library>
    <book id="B001">
        <title>Web Tech</title>
        <pages>300</pages>
    </book>
</library>
```

**DTD**:
```dtd
<!ELEMENT library (book)>
<!ELEMENT book (title, pages)>
<!ELEMENT title (#PCDATA)>
<!ELEMENT pages (#PCDATA)>
<!ATTLIST book id CDATA #REQUIRED>
```

**XSD**:
```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="library">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="book">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="title" type="xs:string"/>
                            <xs:element name="pages" type="xs:integer"/>
                        </xs:sequence>
                        <xs:attribute name="id" type="xs:string" use="required"/>
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```
</details>


#### 5.7 XML Style Sheets (XSLT)
XSLT (**Extensible Stylesheet Language Transformations**) turns XML into something else, like HTML for display.

**Example**:
XML:
```xml
<student>
    <name>John</name>
    <grade>A</grade>
</student>
```
XSLT:
```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:template match="/">
        <html>
            <body>
                <h1><xsl:value-of select="student/name"/></h1>
                <p>Grade: <xsl:value-of select="student/grade"/></p>
            </body>
        </html>
    </xsl:template>
</xsl:stylesheet>
```
Output: A webpage with “John” as a heading and “Grade: A” below it.

---

#### 5.8 XQuery
XQuery is like SQL but for XML. It lets you search and pull data from XML files.

**Example**:
XML:
```xml
<school>
    <student>
        <name>John</name>
        <grade>A</grade>
    </student>
    <student>
        <name>Mary</name>
        <grade>B</grade>
    </student>
</school>
```
XQuery:
```xquery
for $x in doc("school.xml")/school/student
where $x/grade = "A"
return $x/name
```
Output: “John” (it finds students with grade A).

---

### Tips for the Exam
- **Focus on basics**: AJAX (`XMLHttpRequest`), XML syntax, and XSD are big topics.
- **Practice examples**: Write a simple XML file and an AJAX call in your lab.
- **Understand the tree**: Sketch out an XML structure to see parents and children.

---
