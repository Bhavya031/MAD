# Practical-1: Configuring Android Development Environment for Mac

## Step 1 - Setup Java Development Kit (JDK)

You can download the latest version of Java JDK from Oracle’s Java site: [Java SE Downloads](https://www.oracle.com/java/technologies/javase-downloads.html). Follow the given instructions to install and configure the setup on your Mac. Ensure you set `PATH` and `JAVA_HOME` environment variables to refer to the directory that contains `java` and `javac`. Typically, this would be:

```
/Library/Java/JavaVirtualMachines/jdk_version/Contents/Home
```

### Command to set `PATH` and `JAVA_HOME` in the terminal:

```bash
export JAVA_HOME=$(/usr/libexec/java_home)export PATH=$JAVA_HOME/bin:$PATH
```

For permanent changes, add these lines to your shell configuration file (`.zshrc`, `.bash_profile`, or equivalent).

## Step 2 - Setup Android Studio IDE

Check the system requirements for Android Studio on the official website: [Android Studio System Requirements](https://developer.android.com/studio#SystemRequirements). Ensure your Mac meets these requirements.

### Steps:

1. Go to [Android Developer](https://developer.android.com/studio).
2. Select “Download Android Studio for Mac.”
3. Run the downloaded installer and follow the on-screen instructions.
4. During installation, select “Android Studio” and “Android Virtual Device.”
5. Take note of the installation locations (default: `~/Library/Android`).

**_IMAGE:_ Add an image of the Android Studio download page for Mac.**

## Step 3 - Installing Android SDK

Using Homebrew, you can quickly install the Android SDK on macOS.

### Steps:

1.  Open Terminal.
2.  Install Homebrew if it's not already installed:

    ```bash
    /bin/bash -c "$(curl -fsSL <https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh>)"

    ```

3.  Use Homebrew to install the Android SDK:

    ```bash
    brew install --cask android-sdk

    ```

4.  Verify the installation by checking the SDK path:
    The default path will typically be `/usr/local/share/android-sdk`.
        ```bash
        echo $ANDROID_HOME

        ```
5.  Add the following lines to your shell configuration file (`.zshrc`, `.bash_profile`, or equivalent):

    ```bash
    export ANDROID_HOME=/usr/local/share/android-sdk
    export PATH=$ANDROID_HOME/emulator:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools:$PATH

    ```

6.  Restart your terminal or run:

    ```bash
    source ~/.zshrc  # or ~/.bash_profile

    ```

7.  To update or manage the SDK components, you can use:

    ```bash
    sdkmanager --list
    sdkmanager "platform-tools" "platforms;android-30"  # Example to install tools and a specific platform

    ```

**_IMAGE:_ Add an image showing the Terminal output of `brew install --cask android-sdk`.**

Let me know if you'd like further adjustments!

## Step 4 - Create Android Virtual Device (AVD)

To test your Android applications, create an Android Virtual Device (AVD) that emulates a physical device.

### Steps:

1. Open Android Studio.
2. Select **“Tools” > “AVD Manager.”**
3. Click **“Create Virtual Device.”**
4. Choose a device definition (e.g., Pixel 4) and select a system image with the highest API level.
5. Name your AVD and click **“Finish.”**

**_IMAGE:_ Add an image of the AVD Manager interface showing virtual device setup.**

Here's the **description text** for the **Configuring Flutter Development Environment** practical with space for images:

# Practical-2: **Develop an Android application that uses GUI components, Font, and Colors.**

### **main.xml** (XML Layout File)

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    xmlns:app="<http://schemas.android.com/apk/res-auto>" xmlns:tools="<http://schemas.android.com/tools>"
    android:layout_width="match_parent" android:layout_height="match_parent"
    tools:context=".MainActivity">

    <!-- Title TextView -->
    <TextView
        android:id="@+id/titleText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Bhavya's App"
        android:textSize="24sp"
        android:textColor="#2c3e50"
        android:fontFamily="sans-serif"
        android:textStyle="bold"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="20dp" />

    <!-- Name Input Field -->
    <EditText
        android:id="@+id/nameInput"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:hint="Enter your name"
        android:padding="10dp"
        android:fontFamily="sans-serif"
        android:textSize="16sp"
        app:layout_constraintTop_toBottomOf="@id/titleText"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginStart="16dp"
        android:layout_marginEnd="16dp"/>

    <!-- Submit Button -->
    <Button
        android:id="@+id/submitBtn"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="Submit"
        android:textColor="#ffffff"
        android:background="#3498db"
        app:layout_constraintTop_toBottomOf="@id/nameInput"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="20dp"
        android:layout_marginStart="16dp"
        android:layout_marginEnd="16dp" />

    <!-- Cancel Button -->
    <Button
        android:id="@+id/cancelBtn"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="Cancel"
        android:textColor="#ffffff"
        android:background="#e74c3c"
        app:layout_constraintTop_toBottomOf="@id/submitBtn"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="10dp"
        android:layout_marginStart="16dp"
        android:layout_marginEnd="16dp" />

</androidx.constraintlayout.widget.ConstraintLayout>

```

### **MainActivity.java** (Java Activity File)

```java
package com.example.bhavysapp;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    EditText nameInput;
    Button submitBtn, cancelBtn;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize UI components
        nameInput = findViewById(R.id.nameInput);
        submitBtn = findViewById(R.id.submitBtn);
        cancelBtn = findViewById(R.id.cancelBtn);

        // Submit Button click event
        submitBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String name = nameInput.getText().toString();
                if (!name.isEmpty()) {
                    Toast.makeText(MainActivity.this, "Hello, " + name + "!", Toast.LENGTH_SHORT).show();
                } else {
                    Toast.makeText(MainActivity.this, "Please enter your name.", Toast.LENGTH_SHORT).show();
                }
            }
        });

        // Cancel Button click event
        cancelBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                nameInput.setText("");
            }
        });
    }
}

```

## Output:

# Practical-3: **Develop an Android application that uses Layout Managers and Event Listeners.**

### **main.xml** (XML Layout File)

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    xmlns:app="<http://schemas.android.com/apk/res-auto>" xmlns:tools="<http://schemas.android.com/tools>"
    android:layout_width="match_parent" android:layout_height="match_parent"
    tools:context=".MainActivity">

    <!-- Title TextView -->
    <TextView
        android:id="@+id/titleText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Enter Your Info"
        android:textSize="20sp"
        android:textColor="#34495e"
        android:fontFamily="sans-serif-medium"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="40dp" />

    <!-- Name Input TextBox -->
    <EditText
        android:id="@+id/nameInput"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:hint="Enter your name"
        android:padding="10dp"
        android:textSize="16sp"
        android:background="@drawable/edittext_border"
        app:layout_constraintTop_toBottomOf="@id/titleText"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintMarginTop="20dp"
        android:layout_marginHorizontal="20dp" />

    <!-- Email Input TextBox -->
    <EditText
        android:id="@+id/emailInput"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:hint="Enter your email"
        android:padding="10dp"
        android:textSize="16sp"
        android:background="@drawable/edittext_border"
        app:layout_constraintTop_toBottomOf="@id/nameInput"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintMarginTop="20dp"
        android:layout_marginHorizontal="20dp" />

    <!-- Submit Button -->
    <Button
        android:id="@+id/submitButton"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="Submit"
        android:textColor="#ffffff"
        android:backgroundTint="#3498db"
        app:layout_constraintTop_toBottomOf="@id/emailInput"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="20dp"
        android:layout_marginHorizontal="20dp" />

    <!-- Output TextView -->
    <TextView
        android:id="@+id/outputText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Your information will appear here."
        android:textSize="16sp"
        android:textColor="#555555"
        app:layout_constraintTop_toBottomOf="@id/submitButton"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="30dp"
        android:layout_marginHorizontal="20dp" />

</androidx.constraintlayout.widget.ConstraintLayout>

```

### **MainActivity.java** (Java Activity File)

```java
package com.example.textboxinteraction;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    EditText nameInput, emailInput;
    Button submitButton;
    TextView outputText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize views
        nameInput = findViewById(R.id.nameInput);
        emailInput = findViewById(R.id.emailInput);
        submitButton = findViewById(R.id.submitButton);
        outputText = findViewById(R.id.outputText);

        // Set click listener for the Submit button
        submitButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Get the values from the input fields
                String name = nameInput.getText().toString();
                String email = emailInput.getText().toString();

                // Check if both fields are filled
                if (!name.isEmpty() && !email.isEmpty()) {
                    outputText.setText("Name: " + name + ", Email: " + email);
                } else {
                    outputText.setText("Please fill in all fields.");
                }
            }
        });
    }
}

```

## Output:

# Practical-4: Develop a standard calculator Android application to perform basic calculations like addition, subtraction, multiplication, and division.

Here is the updated code:

### **XML Layout (`calculator_layout.xml`):**

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="20dp"
    android:background="#f0f0f0">

    <!-- Display area -->
    <EditText
        android:id="@+id/display"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:padding="20dp"
        android:textSize="30sp"
        android:background="#34495e"
        android:textColor="#ffffff"
        android:gravity="end"
        android:hint="0"
        android:focusable="false"
        android:cursorVisible="false"/>

    <!-- Buttons Grid -->
    <GridLayout
        android:layout_below="@id/display"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:columnCount="4"
        android:rowCount="5"
        android:orientation="vertical">

        <!-- Buttons row 1 -->
        <Button
            android:id="@+id/clear_button"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnSpan="2"
            android:text="C"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#e74c3c"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/number7"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="7"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/number8"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="8"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/number9"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="9"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <!-- Buttons row 2 -->
        <Button
            android:id="@+id/number4"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="4"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/number5"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="5"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/number6"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="6"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <!-- Buttons row 3 -->
        <Button
            android:id="@+id/number1"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="1"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/number2"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="2"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/number3"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="3"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <!-- Buttons row 4 -->
        <Button
            android:id="@+id/number0"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="2"
            android:text="0"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/operator_add"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="+"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/operator_subtract"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="-"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/operator_multiply"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="*"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <Button
            android:id="@+id/operator_divide"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:text="/"
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#16a085"
            android:textColor="#fff"/>

        <!-- Equal Button -->
        <Button
            android:id="@+id/equal_button"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="="
            android:textSize="20sp"
            android:layout_gravity="center"
            android:background="#3498db"
            android:textColor="#fff"/>
    </GridLayout>

</RelativeLayout>

```

### **Java Activity (`CalculatorActivity.java`):**

```java
package com.example.calculator;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.GridLayout;

import androidx.appcompat.app.AppCompatActivity;

public class CalculatorActivity extends AppCompatActivity {

    private EditText display;
    private String currentInput = "";
    private String previousInput = "";
    private String operator = "";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.calculator_layout);

        display = findViewById(R.id.display);

        // Button References
        Button clearButton = findViewById(R.id.clear_button);
        Button button7 = findViewById(R.id.number7);
        Button button8 = findViewById(R.id.number8);
        Button button9 = findViewById(R.id.number9);
        Button button4 = findViewById(R.id.number4);
        Button button5 = findViewById(R.id.number5);
        Button button6 = findViewById(R.id.number6);
        Button button1 = findViewById(R.id.number1);
        Button button2 = findViewById(R.id.number2);
        Button button3 = findViewById(R.id.number3);
        Button button0 = findViewById(R.id.number0);
        Button operatorAdd = findViewById(R.id.operator_add);
        Button operatorSubtract = findViewById(R.id.operator_subtract);
        Button operatorMultiply = findViewById(R.id.operator_multiply);
        Button operatorDivide = findViewById(R.id.operator_divide);
        Button equalButton = findViewById(R.id.equal_button);

        // Setting Click Listeners for Buttons
        clearButton.setOnClickListener(v -> clearDisplay());
        button7.setOnClickListener(v -> appendNumber("7"));
        button8.setOnClickListener(v -> appendNumber("8"));
        button9

.setOnClickListener(v -> appendNumber("9"));
        button4.setOnClickListener(v -> appendNumber("4"));
        button5.setOnClickListener(v -> appendNumber("5"));
        button6.setOnClickListener(v -> appendNumber("6"));
        button1.setOnClickListener(v -> appendNumber("1"));
        button2.setOnClickListener(v -> appendNumber("2"));
        button3.setOnClickListener(v -> appendNumber("3"));
        button0.setOnClickListener(v -> appendNumber("0"));

        operatorAdd.setOnClickListener(v -> setOperator("+"));
        operatorSubtract.setOnClickListener(v -> setOperator("-"));
        operatorMultiply.setOnClickListener(v -> setOperator("*"));
        operatorDivide.setOnClickListener(v -> setOperator("/"));

        equalButton.setOnClickListener(v -> calculateResult());
    }

    private void appendNumber(String number) {
        currentInput += number;
        display.setText(currentInput);
    }

    private void setOperator(String operator) {
        if (!currentInput.isEmpty()) {
            previousInput = currentInput;
            currentInput = "";
            this.operator = operator;
        }
    }

    private void clearDisplay() {
        currentInput = "";
        previousInput = "";
        operator = "";
        display.setText("");
    }

    private void calculateResult() {
        if (!previousInput.isEmpty() && !currentInput.isEmpty() && !operator.isEmpty()) {
            double num1 = Double.parseDouble(previousInput);
            double num2 = Double.parseDouble(currentInput);
            double result = 0;

            switch (operator) {
                case "+":
                    result = num1 + num2;
                    break;
                case "-":
                    result = num1 - num2;
                    break;
                case "*":
                    result = num1 * num2;
                    break;
                case "/":
                    if (num2 != 0) {
                        result = num1 / num2;
                    } else {
                        display.setText("Error");
                        return;
                    }
                    break;
            }

            display.setText(String.valueOf(result));
            previousInput = "";
            currentInput = String.valueOf(result);
        }
    }
}

```

## Output:

# Practical-5: **Develop an Android application to create, save, update, and delete data in a database.**

### `activity_contact_manager.xml` (Layout File)

This is the XML layout for the Android app:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp"
    android:background="#f8f9fa">

    <!-- Title Text -->
    <TextView
        android:id="@+id/titleText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Contact Manager"
        android:textSize="24sp"
        android:textColor="#2c3e50"
        android:layout_gravity="center"
        android:layout_marginBottom="20dp"/>

    <!-- Name Input -->
    <EditText
        android:id="@+id/nameInput"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Name"
        android:padding="10dp"
        android:layout_marginBottom="15dp"
        android:background="#ffffff"
        android:drawableLeft="@android:drawable/ic_menu_edit"
        android:inputType="textPersonName"/>

    <!-- Phone Input -->
    <EditText
        android:id="@+id/phoneInput"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Phone Number"
        android:padding="10dp"
        android:layout_marginBottom="15dp"
        android:background="#ffffff"
        android:inputType="phone"/>

    <!-- Add Contact Button -->
    <Button
        android:id="@+id/addContactButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Add Contact"
        android:layout_gravity="center"
        android:background="#3498db"
        android:textColor="#ffffff"
        android:padding="10dp"/>

    <!-- Contact List -->
    <LinearLayout
        android:id="@+id/contactListLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:layout_marginTop="20dp"/>
</LinearLayout>

```

### `ContactManagerActivity.java` (Java Code)

```java
package com.example.contactmanager;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.LinearLayout;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import java.util.ArrayList;

public class ContactManagerActivity extends AppCompatActivity {

    private EditText nameInput, phoneInput;
    private LinearLayout contactListLayout;
    private ArrayList<Contact> contacts;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_contact_manager);

        // Initialize views
        nameInput = findViewById(R.id.nameInput);
        phoneInput = findViewById(R.id.phoneInput);
        contactListLayout = findViewById(R.id.contactListLayout);
        Button addContactButton = findViewById(R.id.addContactButton);

        // Initialize contact list (preloaded contacts)
        contacts = new ArrayList<>();
        contacts.add(new Contact("John Doe", "123-456-7890"));
        contacts.add(new Contact("Jane Smith", "987-654-3210"));
        contacts.add(new Contact("Emily Davis", "456-789-1234"));

        // Render contacts
        renderContacts();

        // Set up button click listener
        addContactButton.setOnClickListener(v -> addContact());
    }

    // Render the contacts on the screen
    private void renderContacts() {
        contactListLayout.removeAllViews(); // Clear previous list

        for (int i = 0; i < contacts.size(); i++) {
            Contact contact = contacts.get(i);
            LinearLayout contactItem = new LinearLayout(this);
            contactItem.setOrientation(LinearLayout.HORIZONTAL);
            contactItem.setPadding(10, 10, 10, 10);

            TextView contactInfo = new TextView(this);
            contactInfo.setText(contact.getName() + " - " + contact.getPhone());
            contactItem.addView(contactInfo);

            Button deleteButton = new Button(this);
            deleteButton.setText("Delete");
            deleteButton.setOnClickListener(v -> deleteContact(i));
            contactItem.addView(deleteButton);

            contactListLayout.addView(contactItem);
        }
    }

    // Add a new contact
    private void addContact() {
        String name = nameInput.getText().toString().trim();
        String phone = phoneInput.getText().toString().trim();

        if (!name.isEmpty() && !phone.isEmpty()) {
            contacts.add(new Contact(name, phone));
            nameInput.setText("");
            phoneInput.setText("");
            renderContacts();
        } else {
            Toast.makeText(this, "Please fill in both fields", Toast.LENGTH_SHORT).show();
        }
    }

    // Delete a contact
    private void deleteContact(int index) {
        contacts.remove(index);
        renderContacts();
    }

    // Contact class to store contact data
    private static class Contact {
        private String name;
        private String phone;

        public Contact(String name, String phone) {
            this.name = name;
            this.phone = phone;
        }

        public String getName() {
            return name;
        }

        public String getPhone() {
            return phone;
        }
    }
}

```

## Output:

# Practical-6: **Develop an Android application that uses GPS location information.**

### `activity_main.xml` (Layout File)

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:background="#f5f5f5">

    <!-- Title Text -->
    <TextView
        android:id="@+id/titleText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="GPS Location Finder"
        android:textSize="24sp"
        android:textColor="#333"
        android:layout_gravity="center"
        android:layout_marginBottom="20dp"/>

    <!-- Location Display -->
    <TextView
        android:id="@+id/locationText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Your location will appear here..."
        android:textSize="18sp"
        android:padding="10dp"
        android:background="#ffffff"
        android:layout_marginBottom="20dp"
        android:gravity="center"/>

    <!-- Button to Get Location -->
    <Button
        android:id="@+id/fetchLocationButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Get My Location"
        android:background="#16a085"
        android:textColor="#ffffff"
        android:layout_marginBottom="20dp"
        android:textSize="18sp"/>

    <!-- Map Display -->
    <FrameLayout
        android:id="@+id/mapFrame"
        android:layout_width="match_parent"
        android:layout_height="250dp"
        android:layout_marginTop="20dp">
    </FrameLayout>

</LinearLayout>

```

### `MainActivity.java` (Java Code)

```java
package com.example.gpslocationapp;

import android.Manifest;
import android.content.pm.PackageManager;
import android.location.Criteria;
import android.location.Location;
import android.location.LocationListener;
import android.location.LocationManager;
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;

import com.google.android.gms.common.api.Status;
import com.google.android.gms.maps.CameraUpdateFactory;
import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.MapFragment;
import com.google.android.gms.maps.OnMapReadyCallback;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.model.MarkerOptions;

public class MainActivity extends AppCompatActivity implements OnMapReadyCallback {

    private TextView locationText;
    private GoogleMap mMap;
    private LocationManager locationManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        locationText = findViewById(R.id.locationText);
        Button fetchLocationButton = findViewById(R.id.fetchLocationButton);
        fetchLocationButton.setOnClickListener(v -> getLocation());

        // Initialize location manager
        locationManager = (LocationManager) getSystemService(LOCATION_SERVICE);

        // Initialize Google Map
        MapFragment mapFragment = (MapFragment) getFragmentManager().findFragmentById(R.id.mapFrame);
        mapFragment.getMapAsync(this);
    }

    // Function to fetch location
    private void getLocation() {
        // Check for permission
        if (ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED &&
                ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            // Request permission
            ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, 1);
            return;
        }

        locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, 0, 0, locationListener);
    }

    // Location listener for updating the location
    private LocationListener locationListener = new LocationListener() {
        @Override
        public void onLocationChanged(@NonNull Location location) {
            double latitude = location.getLatitude();
            double longitude = location.getLongitude();

            // Update the location text
            locationText.setText(String.format("Latitude: %s\\nLongitude: %s", latitude, longitude));

            // Update the map with the new location
            updateMap(latitude, longitude);
        }

        @Override
        public void onStatusChanged(String provider, int status, Bundle extras) {
        }

        @Override
        public void onProviderEnabled(@NonNull String provider) {
        }

        @Override
        public void onProviderDisabled(@NonNull String provider) {
        }
    };

    // Function to update the map with the current location
    private void updateMap(double latitude, double longitude) {
        LatLng location = new LatLng(latitude, longitude);
        mMap.addMarker(new MarkerOptions().position(location).title("You are here!"));
        mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(location, 12));
    }

    @Override
    public void onMapReady(GoogleMap googleMap) {
        mMap = googleMap;
    }

    // Handle permission request results
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == 1) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                getLocation();
            } else {
                Toast.makeText(this, "Permission denied. Cannot fetch location.", Toast.LENGTH_SHORT).show();
            }
        }
    }
}

```

## Output:

# Practical-7: **Develop an Android application that draws basic graphical primitives (Rectangle, Circle, etc.) on the screen.**

Here's how you can structure this into XML (for layout) and Java code.

### 1. XML Layout (Using `JPanel` for layout)

```xml
<layout>
    <window title="Modern Drawing App" width="800" height="600">
        <panel layout="border" background="#ffffff">

            <!-- Drawing Canvas -->
            <canvas id="drawingCanvas" width="800" height="500" background="#f8f9fa"/>

            <!-- Drawing Controls -->
            <panel layout="horizontal" position="bottom">
                <button id="rectangleBtn" text="Rectangle" background="#f8f9fa" />
                <button id="circleBtn" text="Circle" background="#f8f9fa" />
                <button id="lineBtn" text="Line" background="#f8f9fa" />
                <color-picker id="colorPicker" value="#2b2d42" />
                <button id="clearBtn" text="Clear" background="#f8f9fa" />
            </panel>

            <!-- Width Control -->
            <panel layout="vertical" position="top-right">
                <label text="Width" />
                <number-input id="lineWidth" value="2" min="1" max="20" />
            </panel>
        </panel>
    </window>
</layout>

```

### 2. Java Application Using Swing

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import javax.swing.colorchooser.*;

public class DrawingApp extends JFrame {

    private String currentShape = "rectangle";
    private boolean isDrawing = false;
    private int startX, startY;
    private Canvas canvas;
    private Color currentColor = Color.decode("#2b2d42");
    private int lineWidth = 2;

    public DrawingApp() {
        setTitle("Modern Drawing App");
        setSize(800, 600);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // Initialize canvas
        canvas = new Canvas();
        add(canvas, BorderLayout.CENTER);

        // Add toolbar for shape selection and color picker
        JPanel toolbar = new JPanel();
        toolbar.setLayout(new FlowLayout(FlowLayout.CENTER));

        JButton rectangleBtn = new JButton("Rectangle");
        rectangleBtn.addActionListener(e -> setShape("rectangle"));

        JButton circleBtn = new JButton("Circle");
        circleBtn.addActionListener(e -> setShape("circle"));

        JButton lineBtn = new JButton("Line");
        lineBtn.addActionListener(e -> setShape("line"));

        JButton clearBtn = new JButton("Clear");
        clearBtn.addActionListener(e -> canvas.clear());

        JButton colorPickerBtn = new JButton("Pick Color");
        colorPickerBtn.addActionListener(e -> pickColor());

        // Add buttons to toolbar
        toolbar.add(rectangleBtn);
        toolbar.add(circleBtn);
        toolbar.add(lineBtn);
        toolbar.add(colorPickerBtn);
        toolbar.add(clearBtn);

        add(toolbar, BorderLayout.SOUTH);

        // Add line width control
        JPanel controlPanel = new JPanel();
        JLabel widthLabel = new JLabel("Width");
        JSpinner lineWidthSpinner = new JSpinner(new SpinnerNumberModel(lineWidth, 1, 20, 1));
        lineWidthSpinner.addChangeListener(e -> lineWidth = (int) lineWidthSpinner.getValue());
        controlPanel.add(widthLabel);
        controlPanel.add(lineWidthSpinner);
        controlPanel.setLocation(600, 15); // Place control at top-right corner

        add(controlPanel, BorderLayout.NORTH);
    }

    private void setShape(String shape) {
        currentShape = shape;
    }

    private void pickColor() {
        currentColor = JColorChooser.showDialog(this, "Choose a color", currentColor);
    }

    private class Canvas extends JPanel {

        private Image image;
        private Graphics2D g2d;

        public Canvas() {
            setPreferredSize(new Dimension(800, 500));
            setBackground(Color.decode("#f8f9fa"));

            addMouseListener(new MouseAdapter() {
                @Override
                public void mousePressed(MouseEvent e) {
                    startX = e.getX();
                    startY = e.getY();
                    isDrawing = true;
                }

                @Override
                public void mouseReleased(MouseEvent e) {
                    isDrawing = false;
                }
            });

            addMouseMotionListener(new MouseMotionAdapter() {
                @Override
                public void mouseDragged(MouseEvent e) {
                    if (isDrawing) {
                        drawShape(e.getX(), e.getY());
                    }
                }
            });
        }

        @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            if (image == null) {
                image = createImage(getWidth(), getHeight());
                g2d = (Graphics2D) image.getGraphics();
                g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
            }
            g.drawImage(image, 0, 0, null);
        }

        private void drawShape(int x, int y) {
            g2d.setColor(currentColor);
            g2d.setStroke(new BasicStroke(lineWidth));

            switch (currentShape) {
                case "rectangle":
                    g2d.clearRect(0, 0, getWidth(), getHeight());
                    g2d.drawRect(startX, startY, x - startX, y - startY);
                    break;
                case "circle":
                    int radius = (int) Math.sqrt(Math.pow(x - startX, 2) + Math.pow(y - startY, 2));
                    g2d.clearRect(0, 0, getWidth(), getHeight());
                    g2d.drawOval(startX - radius, startY - radius, 2 * radius, 2 * radius);
                    break;
                case "line":
                    g2d.clearRect(0, 0, getWidth(), getHeight());
                    g2d.drawLine(startX, startY, x, y);
                    break;
            }
            repaint();
        }

        public void clear() {
            image = null;
            repaint();
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            DrawingApp app = new DrawingApp();
            app.setVisible(true);
        });
    }
}

```

## Output:

# **Practical-8: Create an Android application that writes data to an SD card.**

### 1. XML Layout (res/layout/activity_main.xml):

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="<http://schemas.android.com/apk/res/android>"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:background="@android:color/holo_blue_bright"
    android:padding="16dp">

    <TextView
        android:id="@+id/titleText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Save Data to Storage"
        android:textSize="24sp"
        android:textColor="#FF6F61"
        android:fontFamily="sans-serif"
        android:layout_marginBottom="16dp"
        android:gravity="center"/>

    <!-- Spinner to choose storage type -->
    <Spinner
        android:id="@+id/storageSelect"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"
        android:background="@android:color/darker_gray" />

    <!-- EditText for user input data -->
    <EditText
        android:id="@+id/dataInput"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter some data to save..."
        android:background="#2f2f2f"
        android:textColor="#ddd"
        android:padding="16dp"
        android:layout_marginBottom="16dp"/>

    <!-- Save Button -->
    <Button
        android:id="@+id/saveButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Save Data"
        android:background="#FF6F61"
        android:textColor="#FFFFFF"
        android:textSize="18sp"
        android:layout_marginBottom="16dp"/>

    <!-- Status Message -->
    <TextView
        android:id="@+id/statusMessage"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text=""
        android:textSize="16sp"
        android:textColor="#FFCC00"
        android:gravity="center" />
</LinearLayout>

```

### 2. Java Activity (MainActivity.java):

```java
package com.example.savedatastorage;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Spinner;
import android.widget.TextView;
import android.widget.ArrayAdapter;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;

public class MainActivity extends AppCompatActivity {

    private Spinner storageSelect;
    private EditText dataInput;
    private TextView statusMessage;
    private Button saveButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize the UI components
        storageSelect = findViewById(R.id.storageSelect);
        dataInput = findViewById(R.id.dataInput);
        statusMessage = findViewById(R.id.statusMessage);
        saveButton = findViewById(R.id.saveButton);

        // Populate the spinner with options
        ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(this,
                R.array.storage_options, android.R.layout.simple_spinner_item);
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        storageSelect.setAdapter(adapter);

        // Set the button click listener
        saveButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                saveToFile();
            }
        });
    }

    // Function to save the data to file
    private void saveToFile() {
        String data = dataInput.getText().toString();
        String storageType = storageSelect.getSelectedItem().toString();

        if (data.trim().isEmpty()) {
            Toast.makeText(this, "Please enter some data to save.", Toast.LENGTH_SHORT).show();
            return;
        }

        // Update status message while saving
        statusMessage.setText("Saving to " + storageType + "...");

        // Simulate saving the data to internal storage or external storage
        try {
            File storageDir;
            String fileName = "data_" + storageType + ".txt";

            if (storageType.equals("Internal Storage")) {
                storageDir = getFilesDir(); // Internal storage
            } else {
                storageDir = getExternalFilesDir(null); // External storage
            }

            File file = new File(storageDir, fileName);
            FileOutputStream fos = new FileOutputStream(file);
            fos.write(data.getBytes());
            fos.close();

            // Show success message
            statusMessage.setText("Data saved successfully! Check your file.");
        } catch (IOException e) {
            e.printStackTrace();
            statusMessage.setText("Error saving data!");
        }
    }
}

```

### 3. Strings Resource (res/values/strings.xml):

```xml
<resources>
    <string name="app_name">Save Data to Storage</string>
    <string-array name="storage_options">
        <item>Internal Storage</item>
        <item>External (SD) Storage</item>
    </string-array>
</resources>

```

### 4. AndroidManifest.xml:

```xml
<manifest xmlns:android="<http://schemas.android.com/apk/res/android>"
    package="com.example.savedatastorage">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/Theme.AppCompat.Light.DarkActionBar">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>

```

## Output:

# Practical-9: Configuring Flutter Development Environment

## Step 1 - Install Flutter SDK

To start developing with Flutter, you need to install the Flutter SDK on your machine.

### Steps:

1. Go to the official Flutter website: [Flutter Install](https://flutter.dev/docs/get-started/install).
2. Download the latest stable release of Flutter for your operating system (Windows, macOS, or Linux).
3. Extract the zip file to an appropriate location on your machine. For example, on macOS, you can place it in the `/usr/local/flutter` directory.

**IMAGE:** Add an image of the Flutter installation page showing download options for different platforms.

## Step 2 - Set Environment Variables

After downloading the Flutter SDK, you need to set up environment variables so you can run Flutter commands from any terminal window.

### Steps:

1. Open your terminal (Mac/Linux) or Command Prompt (Windows).
2. Add the Flutter binary directory to your system’s `PATH` by updating your `.bash_profile` or `.zshrc` file:

   ```bash
   export PATH="$PATH:`<path-to-flutter-directory>/flutter/bin`"

   ```

3. Run `source ~/.zshrc` or `source ~/.bash_profile` to apply the changes.

**IMAGE:** Add an image of the terminal with the path configuration for Flutter SDK.

## Step 3 - Install Flutter Dependencies

Once the Flutter SDK is installed, you need to run `flutter doctor` to ensure that all dependencies are installed correctly.

### Steps:

1. Open a terminal and run the following command:

   ```bash
   flutter doctor

   ```

2. The `flutter doctor` command checks your environment and displays a report to the terminal window. If any dependencies are missing, it will provide instructions on how to install them.

**IMAGE:** Add an image of the `flutter doctor` terminal output with any missing dependencies highlighted.

## Step 4 - Install Android Studio and Plugins

To develop Flutter apps, it’s recommended to use Android Studio as the IDE.

### Steps:

1. Go to [Android Studio's official download page](https://developer.android.com/studio) and download the appropriate version for your operating system.
2. After downloading, run the installer and follow the on-screen instructions to set up Android Studio.
3. During installation, make sure to select **Flutter** and **Dart** plugins in the setup wizard.

**IMAGE:** Add an image showing the Flutter and Dart plugin installation in Android Studio.

## Step 5 - Create Your First Flutter Project

Now that you have set up the environment, you can create your first Flutter project.

### Steps:

1. Open Android Studio.
2. Go to **File > New > New Flutter Project**.
3. Select **Flutter Application** and click **Next**.
4. Set your project name, and choose the location where it will be saved.
5. Click **Finish** to create the project.

**IMAGE:** Add an image showing the Flutter project creation wizard in Android Studio.

# Practical-10: **Develop a Flutter application that uses GUI components, Font, and Color.**

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter UI Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: HomeScreen(),
    );
  }
}

class HomeScreen extends StatefulWidget {
  @override
  _HomeScreenState createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  TextEditingController _nameController = TextEditingController();
  String _greetingMessage = '';

  void _showGreeting() {
    setState(() {
      String name = _nameController.text;
      _greetingMessage = name.isNotEmpty
          ? 'Hi, $name! Thanks for visiting this Flutter-inspired UI.'
          : 'Please enter your name!';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Color(0xFFF4F6F9),
      body: Center(
        child: Container(
          padding: EdgeInsets.symmetric(vertical: 40, horizontal: 30),
          width: 350,
          decoration: BoxDecoration(
            color: Colors.white,
            borderRadius: BorderRadius.circular(15),
            boxShadow: [
              BoxShadow(
                color: Colors.black.withOpacity(0.1),
                blurRadius: 20,
                offset: Offset(0, 4),
              ),
            ],
          ),
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              Text(
                'Welcome to Flutter UI',
                style: TextStyle(
                  fontSize: 22,
                  fontFamily: 'Poppins',
                  color: Color(0xFF5D5DFF),
                  marginBottom: 20,
                ),
              ),
              Text(
                'Enter your name to get a personalized greeting message:',
                style: TextStyle(fontSize: 16, color: Color(0xFF444444)),
                textAlign: TextAlign.center,
              ),
              SizedBox(height: 25),
              TextField(
                controller: _nameController,
                decoration: InputDecoration(
                  labelText: 'Your Name:',
                  labelStyle: TextStyle(
                    fontSize: 18,
                    color: Color(0xFF333333),
                    fontWeight: FontWeight.bold,
                  ),
                  hintText: 'Type here...',
                  border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(8),
                    borderSide: BorderSide(color: Color(0xFFD3D3D3)),
                  ),
                  focusedBorder: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(8),
                    borderSide: BorderSide(color: Color(0xFF5D5DFF)),
                  ),
                ),
              ),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: _showGreeting,
                child: Text(
                  'Submit',
                  style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
                ),
                style: ElevatedButton.styleFrom(
                  primary: Color(0xFF5D5DFF),
                  padding: EdgeInsets.symmetric(vertical: 12, horizontal: 25),
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(8),
                  ),
                ),
              ),
              SizedBox(height: 20),
              Container(
                padding: EdgeInsets.all(15),
                decoration: BoxDecoration(
                  color: Color(0xFFF2F3F7),
                  borderRadius: BorderRadius.circular(8),
                ),
                child: Text(
                  _greetingMessage,
                  style: TextStyle(
                    fontSize: 18,
                    color: Color(0xFF5D5DFF),
                    fontWeight: FontWeight.bold,
                  ),
                  textAlign: TextAlign.center,
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}

```

## Output:

# Practical-11: **Develop a login-signup application using Flutter.**

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: LoginSignupPage(),
    );
  }
}

class LoginSignupPage extends StatefulWidget {
  @override
  _LoginSignupPageState createState() => _LoginSignupPageState();
}

class _LoginSignupPageState extends State<LoginSignupPage> {
  bool isLogin = true;
  final TextEditingController usernameController = TextEditingController();
  final TextEditingController passwordController = TextEditingController();
  final TextEditingController confirmPasswordController = TextEditingController();

  String errorMessage = '';
  String successMessage = '';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Color(0xFFF0F4F8),
      body: Center(
        child: Container(
          width: 380,
          decoration: BoxDecoration(
            color: Colors.white,
            borderRadius: BorderRadius.circular(12),
            boxShadow: [
              BoxShadow(
                color: Colors.black.withOpacity(0.1),
                offset: Offset(0, 15),
                blurRadius: 40,
              ),
            ],
          ),
          child: Column(
            children: [
              Container(
                padding: EdgeInsets.all(35),
                decoration: BoxDecoration(
                  gradient: LinearGradient(
                    colors: [Color(0xFF4CAF50), Color(0xFF81C784)],
                    begin: Alignment.topLeft,
                    end: Alignment.bottomRight,
                  ),
                  borderRadius: BorderRadius.only(
                    topLeft: Radius.circular(12),
                    topRight: Radius.circular(12),
                  ),
                ),
                child: Text(
                  isLogin ? 'Login' : 'Signup',
                  style: TextStyle(
                    color: Colors.white,
                    fontSize: 24,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              Padding(
                padding: const EdgeInsets.all(30.0),
                child: Column(
                  children: [
                    TextField(
                      controller: usernameController,
                      decoration: InputDecoration(
                        labelText: 'Username',
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(10),
                        ),
                        filled: true,
                        fillColor: Color(0xFFF9F9F9),
                      ),
                    ),
                    SizedBox(height: 20),
                    TextField(
                      controller: passwordController,
                      obscureText: true,
                      decoration: InputDecoration(
                        labelText: 'Password',
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(10),
                        ),
                        filled: true,
                        fillColor: Color(0xFFF9F9F9),
                      ),
                    ),
                    if (!isLogin)
                      SizedBox(height: 20),
                    if (!isLogin)
                      TextField(
                        controller: confirmPasswordController,
                        obscureText: true,
                        decoration: InputDecoration(
                          labelText: 'Confirm Password',
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(10),
                          ),
                          filled: true,
                          fillColor: Color(0xFFF9F9F9),
                        ),
                      ),
                    SizedBox(height: 20),
                    ElevatedButton(
                      onPressed: handleSubmit,
                      child: Text(isLogin ? 'Login' : 'Signup'),
                      style: ElevatedButton.styleFrom(
                        primary: Color(0xFF4CAF50),
                        padding: EdgeInsets.symmetric(vertical: 16),
                        shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(12),
                        ),
                      ),
                    ),
                    SizedBox(height: 20),
                    if (errorMessage.isNotEmpty)
                      Text(
                        errorMessage,
                        style: TextStyle(color: Colors.red),
                      ),
                    if (successMessage.isNotEmpty)
                      Text(
                        successMessage,
                        style: TextStyle(color: Colors.green),
                      ),
                    SizedBox(height: 10),
                    TextButton(
                      onPressed: toggleForm,
                      child: Text(
                        isLogin
                            ? "Don't have an account? Signup"
                            : 'Already have an account? Login',
                        style: TextStyle(color: Color(0xFF388E3C)),
                      ),
                    ),
                  ],
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }

  void handleSubmit() {
    final username = usernameController.text;
    final password = passwordController.text;

    if (isLogin) {
      if (username == 'user' && password == 'password') {
        setState(() {
          successMessage = 'Login successful!';
          errorMessage = '';
        });
      } else {
        setState(() {
          errorMessage = 'Invalid username or password!';
          successMessage = '';
        });
      }
    } else {
      final confirmPassword = confirmPasswordController.text;
      if (password == confirmPassword) {
        setState(() {
          successMessage = 'Signup successful!';
          errorMessage = '';
        });
      } else {
        setState(() {
          errorMessage = 'Passwords do not match!';
          successMessage = '';
        });
      }
    }
  }

  void toggleForm() {
    setState(() {
      isLogin = !isLogin;
      errorMessage = '';
      successMessage = '';
      usernameController.clear();
      passwordController.clear();
      confirmPasswordController.clear();
    });
  }
}

```

## Output:
