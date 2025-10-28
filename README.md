实验2：Android界面布局实验 实验信息 课程名称：移动应用开发

实验编号：实验2

实验名称：Android界面布局实践

学号：121052023045

姓名：林健

实验日期：2025.10.15

实验目标 掌握LinearLayout(线性布局)、TableLayout（表格布局）和ConstraintLayout(约束布局)三种布局的使用方法

理解不同布局的特点和适用场景

学会使用XML编写复杂的用户界面

掌握通过多个Activity分别展示不同布局界面

实验环境 环境组件 版本信息 开发工具 Android Studio Narwhal 3,Gradel 8.13 目标API API 21 开发语言 Java 项目包名 com.example.test02

一、项目设计思路

核心目标:开发一个综合性的Android应用，展示多种UI布局技术的实现方式，同时集成基础功能模块，帮助开发者理解和掌握Android界面设计与交互开发。

主要功能模块
导航系统：主菜单集中管理各功能模块的跳转

布局展示：线性布局、表格布局等核心布局方式的实践演示

交互功能：基础计算器实现，展示事件处理机制

主题界面：太空主题界面，体现Android主题化设计能力

响应式适配：支持不同屏幕尺寸和系统边距的适配

用户需求分析
开发者需要直观了解各种Android布局方式的实际效果

学习者希望通过实例代码掌握Activity间跳转和事件处理

用户期望界面简洁明了，操作流程清晰

应用应具备良好的导航体验和一致性设计

技术选型与实现
架构模式：多Activity架构，主菜单导航模式

布局技术：LinearLayout、TableLayout、ConstraintLayout

交互处理：OnClickListener事件监听

主题系统：AppCompat主题，自定义界面样式

适配方案：WindowInsetsCompat处理系统边距

二、项目功能实现
1. 主菜单导航系统
功能描述：作为应用入口，提供清晰的功能模块导航界面，用户可通过点击按钮快速进入不同功能模块。

实现思路：

使用MainMenuActivity作为启动Activity

通过Intent实现Activity间的显式跳转

按钮点击事件绑定对应的目标Activity

核心代码：
package com.example.test02;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.appcompat.app.AppCompatActivity;

public class MainMenuActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState); // 添加这行
        setContentView(R.layout.activity_main_menu);

        // 获取按钮引用 - 使用正确的ID名称
        Button btnLinearLayout = findViewById(R.id.btn_linear);
        Button btnTableLayout = findViewById(R.id.btn_table);
        Button btnCalculator = findViewById(R.id.btn_calculator);
        Button btnSpace = findViewById(R.id.btn_space);

        // 设置线性布局按钮点击事件
        btnLinearLayout.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainMenuActivity.this, MainActivity.class);
                startActivity(intent);
            }
        });

        // 设置表格布局按钮点击事件
        btnTableLayout.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainMenuActivity.this, TableLayoutActivity.class);
                startActivity(intent);
            }
        });

        // 设置计算器按钮点击事件
        btnCalculator.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainMenuActivity.this, CalculatorActivity.class); // 修复类名
                startActivity(intent);
            }
        });
        btnSpace.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainMenuActivity.this, SpaceActivity.class);
                startActivity(intent);
            }
        });
    } // onCreate 方法结束
} // 类结束

效果展示：
主界面展示四个功能入口按钮，点击后平滑跳转到对应功能界面。
<img width="504" height="1163" alt="9c49af2327f7f70b542f0eb527def1ed" src="https://github.com/user-attachments/assets/19881806-2617-4be3-8195-0fd228dc8cea" />


2. 线性布局展示
功能描述：演示Android线性布局(LinearLayout)的实际应用，展示视图的线性排列方式。

实现思路：

使用LinearLayout作为根布局

通过orientation属性控制排列方向

实现返回导航功能，保持用户体验一致性

核心代码：

package com.example.test02;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 返回主菜单页面事件
        Button btnBack = findViewById(R.id.btn_back);
        btnBack.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finish(); // 关闭当前Activity，返回主菜单
            }
        });

    }
}
布局文件代码：

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="#F5F5F5"
    android:padding="16dp"
    tools:context=".MainActivity">
    <!-- 返回主菜单页面 -->
    <Button
        android:id="@+id/btn_back"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="返回主菜单"
        android:layout_gravity="start"
        android:layout_margin="8dp" />
    <!-- 标题 -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="4x4 linear Layout"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="#333333"
        android:gravity="center"
        android:layout_marginBottom="24dp" />

    <!-- 第一行 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:orientation="horizontal"
        android:layout_marginBottom="8dp">

        <TextView
            android:id="@+id/cell11"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="One,One"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell12"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="One,Two"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell13"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="One,Three"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell14"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="One,Four"
            android:textColor="#333333"
            android:textSize="16sp" />
    </LinearLayout>

    <!-- 第二行 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:orientation="horizontal"
        android:layout_marginBottom="8dp">

        <TextView
            android:id="@+id/cell21"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Two,One"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell22"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Two,Two"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell23"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Two,Three"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell24"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Two,Four"
            android:textColor="#333333"
            android:textSize="16sp" />
    </LinearLayout>

    <!-- 第三行 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:orientation="horizontal"
        android:layout_marginBottom="8dp">

        <TextView
            android:id="@+id/cell31"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Three,One"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell32"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Three,Two"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell33"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Three,Three"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell34"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Three,Four"
            android:textColor="#333333"
            android:textSize="16sp" />
    </LinearLayout>

    <!-- 第四行 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:orientation="horizontal">

        <TextView
            android:id="@+id/cell41"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Four,One"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell42"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Four,Two"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell43"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:layout_marginEnd="8dp"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Four,Three"
            android:textColor="#333333"
            android:textSize="16sp" />

        <TextView
            android:id="@+id/cell44"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:background="@drawable/cell_background"
            android:gravity="center"
            android:text="Four,Four"
            android:textColor="#333333"
            android:textSize="16sp" />
    </LinearLayout>

</LinearLayout>

效果展示：
界面元素按垂直方向线性排列，包含标题文本和返回按钮。
<img width="528" height="1272" alt="ae32dc5b81d6a6b3604acf3e8289d270" src="https://github.com/user-attachments/assets/0853f076-9d2a-4fbd-a19a-67c730dda808" />

3. 表格布局实现
功能描述：展示TableLayout表格布局的使用方法，演示如何创建规整的行列结构界面。

实现思路：

使用TableLayout和TableRow构建表格结构

集成系统边距适配，确保界面在不同设备上正常显示

实现统一的返回导航机制

核心代码：

package com.example.test02;

import android.annotation.SuppressLint;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;


import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class TableLayoutActivity extends AppCompatActivity {

    @SuppressLint("MissingInflatedId")
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_table_layout);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
        // 返回主菜单页面事件
        Button btnBack = findViewById(R.id.btn_back);
        btnBack.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finish(); // 关闭当前Activity，返回主菜单
            }
        });
    }
}

布局文件代码:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="#FFFFFF"
    android:padding="16dp"
    tools:context=".TableLayoutActivity">
    <!-- 返回主菜单页面 -->
    <Button
        android:id="@+id/btn_back"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="返回主菜单"
        android:layout_gravity="start"
        android:layout_margin="8dp" />
    <!-- 标题 -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Hello TableLayout"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="#333333"
        android:gravity="center"
        android:layout_marginBottom="32dp" />

    <!-- 表格布局 -->
    <TableLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:stretchColumns="*"
        android:background="@drawable/table_border">

        <!-- 第一行 -->
        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/row_background">

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Open..."
                android:textSize="16sp"
                android:textColor="#333333"
                android:padding="12dp" />

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Ctrl-O"
                android:textSize="16sp"
                android:textColor="#666666"
                android:padding="12dp"
                android:gravity="end" />
        </TableRow>

        <!-- 第二行 -->
        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/row_background">

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Save..."
                android:textSize="16sp"
                android:textColor="#333333"
                android:padding="12dp" />

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Ctrl-S"
                android:textSize="16sp"
                android:textColor="#666666"
                android:padding="12dp"
                android:gravity="end" />
        </TableRow>

        <!-- 第三行 -->
        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/row_background">

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Save As..."
                android:textSize="16sp"
                android:textColor="#333333"
                android:padding="12dp" />

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Ctrl-Shift-S"
                android:textSize="16sp"
                android:textColor="#666666"
                android:padding="12dp"
                android:gravity="end" />
        </TableRow>

        <!-- 空行分隔 -->
        <TableRow
            android:layout_width="match_parent"
            android:layout_height="1dp"
            android:background="#E0E0E0" />

        <!-- 第四行（带X标记） -->
        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/row_background">

            <LinearLayout
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:orientation="horizontal"
                android:padding="12dp">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="X"
                    android:textSize="16sp"
                    android:textColor="#FF0000"
                    android:layout_marginEnd="8dp" />

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="Import..."
                    android:textSize="16sp"
                    android:textColor="#333333" />
            </LinearLayout>

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text=""
                android:textSize="16sp"
                android:textColor="#666666"
                android:padding="12dp"
                android:gravity="end" />
        </TableRow>

        <!-- 第五行（带X标记） -->
        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/row_background">

            <LinearLayout
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:orientation="horizontal"
                android:padding="12dp">

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="X"
                    android:textSize="16sp"
                    android:textColor="#FF0000"
                    android:layout_marginEnd="8dp" />

                <TextView
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="Export..."
                    android:textSize="16sp"
                    android:textColor="#333333" />
            </LinearLayout>

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Ctrl-E"
                android:textSize="16sp"
                android:textColor="#666666"
                android:padding="12dp"
                android:gravity="end" />
        </TableRow>

        <!-- 空行分隔 -->
        <TableRow
            android:layout_width="match_parent"
            android:layout_height="1dp"
            android:background="#E0E0E0" />

        <!-- 第六行 -->
        <TableRow
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/row_background">

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Quit"
                android:textSize="16sp"
                android:textColor="#333333"
                android:padding="12dp" />

            <TextView
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text=""
                android:textSize="16sp"
                android:textColor="#666666"
                android:padding="12dp"
                android:gravity="end" />
        </TableRow>

    </TableLayout>

</LinearLayout>

效果展示：
界面呈现规整的表格形式，包含多个行和列，适配系统边距。
<img width="525" height="1203" alt="750cf3b0f73f090b40b58fa0da2c74d9" src="https://github.com/user-attachments/assets/ecb9843d-47b5-4189-aaff-0d9cd245f74c" />

4. 计算器功能模块
功能描述：实现基础计算器功能，包含数字输入和基本运算操作，展示复杂交互界面的开发方法。

实现思路：

设计计算器界面布局，包含数字按钮和运算符按钮

实现按钮点击事件监听机制

集成系统边距适配和返回导航功能

核心代码：

package com.example.test02;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class CalculatorActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_calculator);

        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });

        // 设置返回按钮
        Button btnBack = findViewById(R.id.btnBack);
        btnBack.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finish(); // 关闭当前Activity，返回主菜单
            }
        });

        // 添加计算器的功能逻辑
        setupCalculatorButtons();
    }

    private void setupCalculatorButtons() {
        // 获取所有按钮并设置点击事件

        Button btn0 = findViewById(R.id.btn0);
        Button btn1 = findViewById(R.id.btn1);
        Button btn2 = findViewById(R.id.btn2);
        Button btn3 = findViewById(R.id.btn3);
        Button btn4 = findViewById(R.id.btn4);
        Button btn5 = findViewById(R.id.btn5);
        Button btn6 = findViewById(R.id.btn6);
        Button btn7 = findViewById(R.id.btn7);
        Button btn8 = findViewById(R.id.btn8);
        Button btn9 = findViewById(R.id.btn9);
        Button btnPlus1 = findViewById(R.id.btnPlus1);
        Button btnPlus2 = findViewById(R.id.btnPlus2);
        Button btnMultiply = findViewById(R.id.btnMultiply);
        Button btnMinus1 = findViewById(R.id.btnMinus1);
        Button btnMinus2 = findViewById(R.id.btnMinus2);

        // 示例：设置数字按钮点击事件
        View.OnClickListener numberClickListener = new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Button button = (Button) v;
            }
        };

        btn0.setOnClickListener(numberClickListener);
        btn1.setOnClickListener(numberClickListener);
        btn2.setOnClickListener(numberClickListener);
        btn3.setOnClickListener(numberClickListener);
        btn4.setOnClickListener(numberClickListener);
        btn5.setOnClickListener(numberClickListener);
        btn6.setOnClickListener(numberClickListener);
        btn7.setOnClickListener(numberClickListener);
        btn8.setOnClickListener(numberClickListener);
        btn9.setOnClickListener(numberClickListener);
    }
}

布局代码:
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#F5F5F5"
    android:padding="16dp"
    tools:context=".CalculatorActivity">

    <!-- 标题 -->
    <TextView
        android:id="@+id/title"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="ConstraintLayoutTest"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="#333333"
        android:gravity="center"
        android:padding="16dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <!-- 输入显示区域 -->
    <TextView
        android:id="@+id/inputLabel"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="Input"
        android:textSize="16sp"
        android:textColor="#666666"
        android:padding="8dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/title" />

    <!-- 显示结果的TextView -->
    <TextView
        android:id="@+id/resultDisplay"
        android:layout_width="0dp"
        android:layout_height="80dp"
        android:text="0.0"
        android:textSize="32sp"
        android:textColor="#333333"
        android:gravity="end|center_vertical"
        android:background="@drawable/display_background"
        android:padding="16dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/inputLabel" />

    <!-- 第一行按钮：7, 8, 9, + -->
    <Button
        android:id="@+id/btn7"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="7"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btn8"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/resultDisplay"
        app:layout_constraintHorizontal_chainStyle="spread"
        android:layout_marginTop="16dp"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btn8"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="8"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btn9"
        app:layout_constraintStart_toEndOf="@+id/btn7"
        app:layout_constraintTop_toTopOf="@+id/btn7"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btn9"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="9"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btnPlus1"
        app:layout_constraintStart_toEndOf="@+id/btn8"
        app:layout_constraintTop_toTopOf="@+id/btn7"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btnPlus1"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="+"
        android:textSize="20sp"
        android:backgroundTint="#FF9800"
        android:textColor="#FFFFFF"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/btn9"
        app:layout_constraintTop_toTopOf="@+id/btn7" />

    <!-- 第二行按钮：4, 5, 6, × -->
    <Button
        android:id="@+id/btn4"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="4"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btn5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/btn7"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btn5"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="5"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btn6"
        app:layout_constraintStart_toEndOf="@+id/btn4"
        app:layout_constraintTop_toTopOf="@+id/btn4"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btn6"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="6"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btnMultiply"
        app:layout_constraintStart_toEndOf="@+id/btn5"
        app:layout_constraintTop_toTopOf="@+id/btn4"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btnMultiply"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="×"
        android:textSize="20sp"
        android:backgroundTint="#FF9800"
        android:textColor="#FFFFFF"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/btn6"
        app:layout_constraintTop_toTopOf="@+id/btn4" />

    <!-- 第三行按钮：1, 2, 3, + -->
    <Button
        android:id="@+id/btn1"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="1"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btn2"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/btn4"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btn2"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="2"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btn3"
        app:layout_constraintStart_toEndOf="@+id/btn1"
        app:layout_constraintTop_toTopOf="@+id/btn1"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btn3"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="3"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btnPlus2"
        app:layout_constraintStart_toEndOf="@+id/btn2"
        app:layout_constraintTop_toTopOf="@+id/btn1"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btnPlus2"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="+"
        android:textSize="20sp"
        android:backgroundTint="#FF9800"
        android:textColor="#FFFFFF"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/btn3"
        app:layout_constraintTop_toTopOf="@+id/btn1" />

    <!-- 第四行按钮：0, -, - -->
    <Button
        android:id="@+id/btn0"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="0"
        android:textSize="20sp"
        android:backgroundTint="#FFFFFF"
        android:textColor="#333333"
        app:layout_constraintEnd_toStartOf="@+id/btnMinus1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/btn1"
        android:layout_marginTop="8dp"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btnMinus1"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="-"
        android:textSize="20sp"
        android:backgroundTint="#FF9800"
        android:textColor="#FFFFFF"
        app:layout_constraintEnd_toStartOf="@+id/btnMinus2"
        app:layout_constraintStart_toEndOf="@+id/btn0"
        app:layout_constraintTop_toTopOf="@+id/btn0"
        android:layout_marginEnd="8dp" />

    <Button
        android:id="@+id/btnMinus2"
        android:layout_width="0dp"
        android:layout_height="60dp"
        android:text="-"
        android:textSize="20sp"
        android:backgroundTint="#FF9800"
        android:textColor="#FFFFFF"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/btnMinus1"
        app:layout_constraintTop_toTopOf="@+id/btn0" />

    <!-- 返回按钮 -->
    <Button
        android:id="@+id/btnBack"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="返回主菜单"
        android:layout_margin="8dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintBottom_toBottomOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>

效果展示：
计算器界面包含0-9数字按钮、加减乘除运算符按钮，支持基础数学运算。
<img width="536" height="1201" alt="8d2d77fbe6eed62475e7075a967753b6" src="https://github.com/user-attachments/assets/b84c1d0d-b3e3-4dd9-8eea-38ede2eda41c" />

5. 太空主题界面
功能描述：展示主题化界面设计，通过太空主题体现Android界面美化和个性化定制能力。

实现思路：

创建专门的太空主题布局文件

使用相关图片资源和颜色方案

保持统一的导航体验

核心代码：
package com.example.test02;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import androidx.appcompat.app.AppCompatActivity;

public class SpaceActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 确保这行加载的是太空主题布局
        setContentView(R.layout.activity_space);

        // 返回主菜单页面事件
        Button btnBack = findViewById(R.id.btnBack);
        btnBack.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finish(); // 关闭当前Activity，返回主菜单
            }
        });
    }
}

布局代码:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="@drawable/galaxy"
    tools:context=".SpaceActivity">
    <!-- 返回按钮 -->
    <Button
        android:id="@+id/btnBack"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="返回主菜单"
        android:layout_gravity="center"
        android:layout_margin="16dp"
        android:padding="12dp" />
    <!-- 标题栏 -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Space Stations"
        android:textSize="32sp"
        android:textStyle="bold"
        android:textColor="#FFFFFF"
        android:gravity="center"
        android:padding="24dp"
        android:background="#40000000" />

    <!-- Flights 部分 -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Flights"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="#FFFFFF"
        android:padding="16dp"
        android:background="#30000000" />

    <!-- 内容区域 -->

    <!-- 底部 Mars 部分 -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:background="#20000000"
        android:orientation="vertical"
        android:padding="16dp">

        <!-- 这里可以添加航班列表或其他内容 -->
        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="12dp"
            android:text="Orbital Station Alpha"
            android:textColor="#FFFFFF"
            android:textSize="18sp" />

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="12dp"
            android:text="Lunar Base Beta"
            android:textColor="#FFFFFF"
            android:textSize="18sp" />

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:background="#50000000"
        android:padding="16dp">

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="MARS"
            android:textSize="24sp"
            android:textStyle="bold"
            android:textColor="#FF6B6B"
            android:gravity="start" />

        <Button
            android:id="@+id/btnDepart"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="DEPART"
            android:textSize="18sp"
            android:textStyle="bold"
            android:textColor="#FFFFFF"
            android:backgroundTint="#FF6B6B"
            android:padding="16dp" />

    </LinearLayout>



</LinearLayout>

效果展示：
太空主题界面，包含相关的视觉元素和背景，提供沉浸式的主题体验。
<img width="521" height="1301" alt="79f607a744de9409a0b3a57f80e7d3bb" src="https://github.com/user-attachments/assets/131217b7-b7a7-4a44-86a1-54d4e0e77aeb" />

三、关键技术细节
1. 应用配置管理
AndroidManifest.xml配置：

xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.test02">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/Theme.AppCompat.Light.DarkActionBar">
        <activity
            android:name=".CalculatorActivity"
            android:exported="false" />
        <!-- 将MainMenuActivity设置为启动Activity -->
        <activity
            android:name=".MainMenuActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity> <!-- 修改MainActivity，移除启动器属性 -->
        <activity
            android:name=".MainActivity"
            android:exported="false" />
        <activity
            android:name=".TableLayoutActivity"
            android:exported="false" />
        <activity
            android:name=".SpaceActivity"
            android:exported="false" />
    </application>

</manifest>

2. 导航架构设计
集中式导航：主菜单作为所有功能的枢纽

显式Intent跳转：明确的Activity间通信

一致的返回体验：每个功能模块都提供返回主菜单的途径

3. 布局技术应用
多种布局方式：LinearLayout、TableLayout等

响应式设计：适配不同屏幕尺寸

系统边距处理：使用WindowInsetsCompat确保界面完整显示

四、项目亮点与扩展方向
1. 项目亮点
教学价值突出：清晰展示各种Android布局技术的实际应用

代码结构清晰：模块化设计，便于理解和学习

用户体验良好：统一的导航模式和一致的操作逻辑

技术覆盖全面：涵盖Activity生命周期、事件处理、界面布局等核心概念

2. 后续优化方向
功能完善：为计算器添加完整的运算逻辑和结果显示

界面优化：增加动画效果和过渡动画提升用户体验

主题扩展：提供更多主题选择，支持用户个性化定制

代码优化：引入ViewModel和LiveData改进架构设计

测试覆盖：添加单元测试和界面测试确保代码质量

3. 学习价值
本项目作为Android开发学习案例，具有以下教育意义：

帮助初学者理解Android多Activity应用架构

展示不同布局方式的适用场景和实现方法

演示标准的Android开发模式和最佳实践

提供可扩展的代码基础，便于在此基础上进行功能扩展

实验源码地址:http://github.com/L-part05/test02
