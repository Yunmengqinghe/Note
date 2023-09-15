## 一、代码设计
1. dialog.h文件
```cpp
#ifndef DIALOG_H
#define DIALOG_H

#include <QDialog>
#include <QCheckBox>
#include <QPushButton>
#include <QPlainTextEdit>
#include <QRadioButton>

class Dialog : public QDialog
{
    Q_OBJECT

public:
    Dialog(QWidget *parent = nullptr);
    ~Dialog();

private slots:
    void do_checkBoxUnline(bool clicked);
    void do_checkBoxItalic(bool clicked);
    void do_checkBoxBold(bool clicked);
    void do_changeTextEdit();

private:
    QCheckBox* chkBoxUnline;
    QCheckBox* chkBoxItalic;
    QCheckBox* chkBoxBold;

    QRadioButton* radioBlack;
    QRadioButton* radioBlue;
    QRadioButton* radioRed;

    QPlainTextEdit* textEdit;

    QPushButton* bottonOK;
    QPushButton* bottonExit;
    QPushButton* bottonCancle;
};
#endif // DIALOG_H
```

2. dialog.cpp文件
```cpp
#include "dialog.h"
#include <QHBoxLayout>
#include <QVBoxLayout>

Dialog::Dialog(QWidget *parent): QDialog(parent)
{
    chkBoxUnline = new QCheckBox("下划线");
    chkBoxItalic = new QCheckBox("斜体");
    chkBoxBold = new QCheckBox("加粗");
    QHBoxLayout* hLayout_1 = new QHBoxLayout();
    hLayout_1->addWidget(chkBoxUnline);
    hLayout_1->addWidget(chkBoxItalic);
    hLayout_1->addWidget(chkBoxBold);

    radioBlack = new QRadioButton("黑色");
    radioBlue = new QRadioButton("蓝色");
    radioRed = new QRadioButton("红色");
    QHBoxLayout* hLayout_2 = new QHBoxLayout();
    hLayout_2->addWidget(radioBlack);
    hLayout_2->addWidget(radioBlue);
    hLayout_2->addWidget(radioRed);

    textEdit = new QPlainTextEdit("Hello World");
    QFont textFont = textEdit->font();
    textFont.setPointSize(20);
    textEdit->setFont(textFont);

    bottonOK = new QPushButton("确定");
    bottonCancle = new QPushButton("取消");
    bottonExit = new QPushButton("退出");
    QHBoxLayout* hLayout_3 = new QHBoxLayout();
    hLayout_3->addWidget(bottonOK);
    hLayout_3->addWidget(bottonCancle);
    hLayout_3->addStretch();
    hLayout_3->addWidget(bottonExit);

    QVBoxLayout* vLayout = new QVBoxLayout();
    vLayout->addLayout(hLayout_1);
    vLayout->addLayout(hLayout_2);
    vLayout->addWidget(textEdit);
    vLayout->addLayout(hLayout_3);

    setLayout(vLayout);

    connect(chkBoxUnline,SIGNAL(clicked(bool)),this,SLOT(do_checkBoxUnline(bool)));
    connect(chkBoxItalic,SIGNAL(clicked(bool)),this,SLOT(do_checkBoxItalic(bool)));
    connect(chkBoxBold,SIGNAL(clicked(bool)),this,SLOT(do_checkBoxBold(bool)));

    connect(radioBlack,SIGNAL(clicked(bool)),this,SLOT(do_changeTextEdit()));connect(radioBlue,SIGNAL(clicked(bool)),this,SLOT(do_changeTextEdit()));connect(radioRed,SIGNAL(clicked(bool)),this,SLOT(do_changeTextEdit()));
connect(bottonOK,SIGNAL(clicked(bool)),this,SLOT(accept()));connect(bottonCancle,SIGNAL(clicked(bool)),this,SLOT(reject()));connect(bottonExit,SIGNAL(clicked(bool)),this,SLOT(close()));

    setWindowTitle("写字板");
}

Dialog::~Dialog()
{
}

void Dialog::do_checkBoxUnline(bool clicked)
{
    QFont textFont = textEdit->font();
    textFont.setUnderline(clicked);
    textEdit->setFont(textFont);
}

void Dialog::do_checkBoxItalic(bool clicked)
{
    QFont textFont = textEdit->font();
    textFont.setItalic(clicked);
    textEdit->setFont(textFont);
}

void Dialog::do_checkBoxBold(bool clicked)
{
    QFont textFont = textEdit->font();
    textFont.setBold(clicked);
    textEdit->setFont(textFont);
}

void Dialog::do_changeTextEdit()
{
    QPalette plet = textEdit->palette();
    if(radioBlack->isChecked())
    {
        plet.setColor(QPalette::Text,Qt::black);
    }
    else if(radioBlue->isChecked())
    {
        plet.setColor(QPalette::Text,Qt::blue);
    }
    else if(radioRed->isChecked())
    {
        plet.setColor(QPalette::Text,Qt::red);
    }
    textEdit->setPalette(plet);
}

```