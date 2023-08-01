# Word
## 参考资料
* [baeldung](https://www.baeldung.com/java-microsoft-word-with-apache-poi)
## XWPFRun
* 一个XWPFParagraph可以有多个Run，分别对应一段中的一部分，这些小部分可以设置不同的样式
## CT系列
* CTSdtBlock ： w:sdt
    * CTSdtContentBlock: w:sdtcontent
## XML
* w:tc :tablecell
* w:p : paragraph
    * w:pPr:paragraph property
* w:hyperlink
    * 实现目录跳转的注意事项
    w:hyperlink中w:ancher属性值要与w:bookmarkStart中w:name保持一致
    w:bookmarkStart中的id和w:bookmarkEnd成对出现，并且id属性必须要有且保持一致

## Q
### 手搓目录
* [使用poi不太可能](https://stackoverflow.com/questions/76449061/how-to-update-page-numbers-in-table-of-contents-toc-or-create-a-toc-with-page)
### poi section
封面不加header，目录不加footer，正文部分都要加

```java
document.getDocument().getBody().addNewSectPr(); //在w:body结束之前加</w:sectPr>

paragraph.getCTP().addNewPPr().addNewSectPr();//才能真正实现section分隔符的效果
```

```java
XWPFHeaderFooterPolicy.createHeader(XWPFHeaderFooterPolicy.DEFAULT, parsHeader);
与
XWPFDocument.createHeader()
之间的区别

1、通过policy.createHeader会直接定位到body前的sectionpr标签(通过parsHeader->document->CTdocument->body->secpr)
```
