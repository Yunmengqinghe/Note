## 一、界面介绍
1. 双击界面文件的.ui文件
![[Pasted image 20230914154852.png]]

2. 介绍
	+ 左侧是工具箱，包含各种组件
	+ 右上是界面中已有的对象，右下是单个组件的属性设置
	+ 中上是界面的可视化图，中下是信号与槽的设计器

## 二、使用.ui文件设计界面

1. 在左侧组件栏中选择组件
2. 设计好属性之后设置信号与槽
![[Pasted image 20230914161631.png]]

## 三、代码设计
1. dialog.h文件
```cpp
#ifndef DIALOG_H
#define DIALOG_H

#include <QDialog>

QT_BEGIN_NAMESPACE
namespace Ui { class Dialog; }
QT_END_NAMESPACE

class Dialog : public QDialog
{
    Q_OBJECT

public:
    Dialog(QWidget *parent = nullptr);
    ~Dialog();

//槽函数，为组件提供反馈
private slots:
    void on_pushButton_Clean_clicked();

    void on_checkBox_DrawLine_clicked(bool checked);

    void on_checkBox_Italic_clicked(bool checked);

    void on_checkBox_Bold_clicked(bool checked);

    void do_FontColor();

private:
    Ui::Dialog *ui;
};
#endif // DIALOG_H
```

2. dialog.cpp文件
```cpp
#include "dialog.h"
#include "ui_dialog.h"

Dialog::Dialog(QWidget *parent)
    : QDialog(parent), ui(new Ui::Dialog)
{
	//展示Ui界面
    ui->setupUi(this);

	//链接函数，将信号和槽相连接
    connect(ui->radioButton_Black, SIGNAL(clicked()), this, SLOT(do_FontColor()));
    connect(ui->radioButton_Blue, SIGNAL(clicked()), this, SLOT(do_FontColor()));
    connect(ui->radioButton_Red, SIGNAL(clicked()), this, SLOT(do_FontColor()));
}

Dialog::~Dialog()
{
    delete ui;
}

void Dialog::on_pushButton_Clean_clicked()
{
    ui->plainTextEdit->clear();
}

//设置字体
void Dialog::on_checkBox_DrawLine_clicked(bool checked)
{
    QFont font = ui->plainTextEdit->font();
    font.setUnderline(checked);
    ui->plainTextEdit->setFont(font);
}

void Dialog::on_checkBox_Italic_clicked(bool checked)
{
    QFont font = ui->plainTextEdit->font();
    font.setItalic(checked);
    ui->plainTextEdit->setFont(font);
}

void Dialog::on_checkBox_Bold_clicked(bool checked)
{
    QFont font = ui->plainTextEdit->font();
    font.setBold(checked);
    ui->plainTextEdit->setFont(font);
}

//设置颜色
void Dialog::do_FontColor()
{
    QPalette plet = ui->plainTextEdit->palette();
    if(ui->radioButton_Black->isChecked())
        plet.setColor(QPalette::Text,Qt::black);
    if(ui->radioButton_Blue->isChecked())
        plet.setColor(QPalette::Text,Qt::blue);
    if(ui->radioButton_Red->isChecked())
        plet.setColor(QPalette::Text,Qt::red);

    ui->plainTextEdit->setPalette(plet);
}
```