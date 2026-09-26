# Демонстрация git diff — UML Activity Diagram (.drawio)

Ниже вывод команды `git diff` для файла `activity.drawio` после добавления
нового действия "Записать результат оплаты в лог".

```diff
diff --git a/lab1/diagrams/activity.drawio b/lab1/diagrams/activity.drawio
index 88f8a50..0e19139 100644
--- a/lab1/diagrams/activity.drawio
+++ b/lab1/diagrams/activity.drawio
@@ -1,73 +1,61 @@
 <mxfile host="app.diagrams.net">
   <diagram name="Activity - Оплата заказа" id="activity1">
-    <mxGraphModel dx="800" dy="600" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="850" pageHeight="1100" math="0" shadow="0">
+    <mxGraphModel dx="1095" dy="620" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="850" pageHeight="1100" math="0" shadow="0">
       <root>
         <mxCell id="0" />
         <mxCell id="1" parent="0" />
-
-        <!-- Начальный узел -->
-        <mxCell id="start" value="" style="ellipse;whiteSpace=wrap;html=1;fillColor=#000000;strokeColor=#000000;" vertex="1" parent="1">
-          <mxGeometry x="380" y="40" width="30" height="30" as="geometry" />
-        </mxCell>
-
-        <!-- Действие 1 -->
-        <mxCell id="act1" value="Клиент вводит данные карты" style="rounded=1;whiteSpace=wrap;html=1;arcSize=40;" vertex="1" parent="1">
-          <mxGeometry x="300" y="110" width="180" height="60" as="geometry" />
-        </mxCell>
+        <mxCell id="start" parent="1" style="ellipse;whiteSpace=wrap;html=1;fillColor=#000000;strokeColor=#000000;" value="" vertex="1">
+          <mxGeometry height="30" width="30" x="380" y="40" as="geometry" />
+        </mxCell>
+        <mxCell id="act1" parent="1" style="rounded=1;whiteSpace=wrap;html=1;arcSize=40;" value="Клиент вводит данные карты" vertex="1">
+          <mxGeometry height="60" width="180" x="300" y="110" as="geometry" />
+        </mxCell>
+        <mxCell id="act6" parent="1" style="rounded=1;whiteSpace=wrap;html=1;arcSize=40;" value="Записать результат оплаты в лог" vertex="1">
+          <mxGeometry height="60" width="180" x="500" y="320" as="geometry" />
+        </mxCell>
         ... (аналогичные строки для остальных элементов) ...
```

*(Полный вывод diff занял более 70 строк — в отчёт помещён показательный
фрагмент; ключевой добавленный блок — элемент `act6`, "Записать результат
оплаты в лог", и связанная с ним стрелка `e9`.)*

## Вывод по демонстрации

Diff для `.drawio` (тоже XML-формат) технически читаем, но оказался куда
"шумнее", чем для `.bpmn`: редактор draw.io при повторном сохранении
переставил порядок атрибутов внутри тегов (например, было
`value="..." style="..." vertex="1" parent="1"`, стало
`parent="1" style="..." value="..." vertex="1"`). Из-за этого Git помечает
как изменённые даже те строки, где по сути ничего не изменилось, кроме
порядка атрибутов. Это показывает важный нюанс: XML-редакторы могут
"шуметь" в diff, даже если реальных изменений немного, и затрудняют чтение
истории изменений.
