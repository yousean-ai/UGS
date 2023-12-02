To extend UGS you can write those features as a new module. 

```
mkdir ugs-platform/ugs-platform-plugin-mymodule
mkdir -p ugs-platform/ugs-platform-plugin-mymodule/src/main/java/com/willwinder/ugs/nbp/mymodule
mkdir -p ugs-platform/ugs-platform-plugin-mymodule/src/main/resources/com/willwinder/ugs/nbp/mymodule
mkdir -p ugs-platform/ugs-platform-plugin-mymodule/src/test/java/com/willwinder/ugs/nbp/mymodule
mkdir ugs-platform/ugs-platform-plugin-mymodule/src/nbm
```

Create a maven module file: `ugs-platform/ugs-platform-plugin-mymodule/pom.xml`
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.willwinder</groupId>
        <artifactId>ugs-platform-parent</artifactId>
        <version>${revision}${changelist}</version>
    </parent>

    <artifactId>ugs-platform-plugin-mymodule</artifactId>
    <packaging>nbm</packaging>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.netbeans.utilities</groupId>
                <artifactId>nbm-maven-plugin</artifactId>
                <extensions>true</extensions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
    <dependencies>
        <dependency>
            <groupId>${project.groupId}</groupId>
            <artifactId>ugs-platform-ugslib</artifactId>
            <version>${project.version}</version>
            <type>jar</type>
        </dependency>
        <dependency>
            <groupId>com.willwinder.universalgcodesender</groupId>
            <artifactId>ugs-core</artifactId>
            <version>${project.version}</version>
            <type>jar</type>
            <scope>provided</scope>
        </dependency>

        <-- NetBeans -->
        <dependency>
            <groupId>org.netbeans.api</groupId>
            <artifactId>org-netbeans-api-annotations-common</artifactId>
            <version>${netbeans.version}</version>
        </dependency>
        <dependency>
            <groupId>org.netbeans.api</groupId>
            <artifactId>org-openide-awt</artifactId>
            <version>${netbeans.version}</version>
            <type>jar</type>
        </dependency>
        <dependency>
            <groupId>org.netbeans.api</groupId>
            <artifactId>org-openide-windows</artifactId>
            <version>${netbeans.version}</version>
            <type>jar</type>
        </dependency>
        <dependency>
            <groupId>org.netbeans.api</groupId>
            <artifactId>org-openide-util</artifactId>
            <version>${netbeans.version}</version>
            <type>jar</type>
        </dependency>
        <dependency>
            <groupId>org.netbeans.api</groupId>
            <artifactId>org-openide-util-lookup</artifactId>
            <version>${netbeans.version}</version>
        </dependency>
        <dependency>
            <groupId>org.netbeans.api</groupId>
            <artifactId>org-openide-util-ui</artifactId>
            <version>${netbeans.version}</version>
        </dependency>
        <dependency>
            <groupId>org.netbeans.api</groupId>
            <artifactId>org-netbeans-modules-options-api</artifactId>
            <version>${netbeans.version}</version>
        </dependency>
        <dependency>
            <groupId>org.netbeans.api</groupId>
            <artifactId>org-netbeans-modules-settings</artifactId>
            <version>${netbeans.version}</version>
        </dependency>

        <!-- UI -->
        <dependency>
            <groupId>com.miglayout</groupId>
            <artifactId>miglayout</artifactId>
            <version>${miglayout.version}</version>
        </dependency>
    </dependencies>
</project>
```

Create bundle properties `ugs-platform/ugs-platform-plugin-mymodule/src/main/resources/com/willwinder/ugs/nbp/mymodule/Bundle.properties`:
```properties
OpenIDE-Module-Name = UGS My Module
OpenIDE-Module-Display-Category = UGS Plugin
OpenIDE-Module-Short-Description = Provides a module to UGS
OpenIDE-Module-Long-Description = <p>A plugin that will provide module for the Universal Gcode Sender.</p>
```

Create netbeans manifest `ugs-platform/ugs-platform-plugin-mymodule/src/main/nbm/manifest.mf`:
```
Manifest-Version: 1.0
OpenIDE-Module-Localizing-Bundle: com/willwinder/ugs/nbp/mymodule/Bundle.properties
OpenIDE-Module-Java-Dependencies: Java > 1.8
OpenIDE-Module-Specification-Version: ${ugs.modules.specification.version}
AutoUpdate-Essential-Module: false

```

Create TopComponent: `ugs-platform/ugs-platform-plugin-mymodule/src/main/resources/com/willwinder/ugs/nbp/mymodule/MyModuleTopComponent.java`
```java
package com.willwinder.ugs.nbp.mymodule;

import com.willwinder.ugs.nbp.lib.Mode;
import com.willwinder.ugs.nbp.lib.lookup.CentralLookup;
import com.willwinder.ugs.nbp.lib.services.LocalizingService;
import com.willwinder.universalgcodesender.i18n.Localization;
import com.willwinder.universalgcodesender.listeners.UGSEventListener;
import com.willwinder.universalgcodesender.model.BackendAPI;
import com.willwinder.universalgcodesender.model.UGSEvent;
import com.willwinder.universalgcodesender.model.events.ControllerStateEvent;
import org.openide.awt.ActionID;
import org.openide.awt.ActionReference;
import org.openide.windows.TopComponent;

import javax.swing.JLabel;
import javax.swing.SwingConstants;
import java.awt.BorderLayout;

@TopComponent.Description(
        preferredID = "MyModuleTopComponent"
)
@TopComponent.Registration(
        mode = Mode.LEFT_BOTTOM,
        openAtStartup = false)
@ActionID(
        category = LocalizingService.CATEGORY_WINDOW,
        id = MyModuleTopComponent.ACTION_ID)
@ActionReference(
        path = LocalizingService.MENU_WINDOW_PLUGIN)
@TopComponent.OpenActionRegistration(
        displayName = "My module",
        preferredID = "MyModuleTopComponent"
)
public final class MyModuleTopComponent extends TopComponent implements UGSEventListener {
    public static final String ACTION_ID = "com.willwinder.ugs.nbp.mymodule.MyModuleTopComponent";
    private final transient BackendAPI backend;

    private final JLabel status = new JLabel();

    public MyModuleTopComponent() {
        backend = CentralLookup.getDefault().lookup(BackendAPI.class);
    }

    @Override
    protected void componentClosed() {
        super.componentClosed();
        backend.removeUGSEventListener(this);
    }

    @Override
    protected void componentOpened() {
        super.componentOpened();
        initComponents();

        setName(Localization.getString("platform.plugin.mymodule.name"));
        setToolTipText(Localization.getString("platform.plugin.mymodule.tooltip"));
        backend.addUGSEventListener(this);
    }

    private void initComponents() {
        removeAll();
        setLayout(new BorderLayout());

        status.setHorizontalAlignment(SwingConstants.CENTER);
        status.setText(backend.getControllerState().name());
        add(status, BorderLayout.CENTER);
    }

    @Override
    public void UGSEvent(UGSEvent event) {
        if (event instanceof ControllerStateEvent controllerStateEvent) {
            status.setText(controllerStateEvent.getState().name());
        }
    }
}

```


Add module as a child module `ugs-platform/pom.xml`
```xml
  <modules>
    ...
    <module>ugs-platform-plugin-mymodule</module>
  </modules>
```

Add as a dependency `ugs-platform/application/pom.xml`
```xml
  <dependencies>
    ...
    <dependency>
      <groupId>${project.groupId}</groupId>
      <artifactId>ugs-platform-plugin-mymodule</artifactId>
      <version>${project.version}</version>
    </dependency>
  </dependencies>
```