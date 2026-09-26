# Демонстрация git diff — текстовый файл (.bpmn)

Ниже показан вывод команды `git diff` для файла `process.bpmn` после добавления
новой промежуточной задачи "Уведомить клиента о начале готовки". Так как это
текстовый XML-формат, Git показывает построчные изменения: что было удалено (`-`)
и что добавлено (`+`).

```diff
diff --git a/lab1/diagrams/process.bpmn b/lab1/diagrams/process.bpmn
index 7d2260e..e363e64 100644
--- a/lab1/diagrams/process.bpmn
+++ b/lab1/diagrams/process.bpmn
@@ -48,8 +48,14 @@
       <bpmn:incoming>Flow_ToEndCancel</bpmn:incoming>
     </bpmn:endEvent>

-    <bpmn:parallelGateway id="Gateway_ParallelSplit" name="Разделение">
+    <!-- НОВЫЙ ЭЛЕМЕНТ: промежуточная задача -->
+    <bpmn:task id="Task_NotifyClient" name="Уведомить клиента о начале готовки">
       <bpmn:incoming>Flow_5_Yes</bpmn:incoming>
+      <bpmn:outgoing>Flow_5b</bpmn:outgoing>
+    </bpmn:task>
+
+    <bpmn:parallelGateway id="Gateway_ParallelSplit" name="Разделение">
+      <bpmn:incoming>Flow_5b</bpmn:incoming>
       <bpmn:outgoing>Flow_6_Cook</bpmn:outgoing>
       <bpmn:outgoing>Flow_6_Courier</bpmn:outgoing>
     </bpmn:parallelGateway>
@@ -86,7 +92,8 @@
     <bpmn:sequenceFlow id="Flow_Back" sourceRef="Task_ChangeOrder" targetRef="Task_Pay" />
     <bpmn:sequenceFlow id="Flow_4" sourceRef="Task_Pay" targetRef="Gateway_Payment" />
     <bpmn:sequenceFlow id="Flow_5_No" name="Нет" sourceRef="Gateway_Payment" targetRef="Task_CancelOrder" />
-    <bpmn:sequenceFlow id="Flow_5_Yes" name="Да" sourceRef="Gateway_Payment" targetRef="Gateway_ParallelSplit" />
+    <bpmn:sequenceFlow id="Flow_5_Yes" name="Да" sourceRef="Gateway_Payment" targetRef="Task_NotifyClient" />
+    <bpmn:sequenceFlow id="Flow_5b" sourceRef="Task_NotifyClient" targetRef="Gateway_ParallelSplit" />
     <bpmn:sequenceFlow id="Flow_ToEndCancel" sourceRef="Task_CancelOrder" targetRef="EndEvent_Cancel" />
     <bpmn:sequenceFlow id="Flow_6_Cook" sourceRef="Gateway_ParallelSplit" targetRef="Task_Cook" />
     <bpmn:sequenceFlow id="Flow_6_Courier" sourceRef="Gateway_ParallelSplit" targetRef="Task_FindCourier" />
@@ -132,28 +139,32 @@
         <dc:Bounds x="662" y="442" width="36" height="36" />
       </bpmndi:BPMNShape>

+      <bpmndi:BPMNShape id="Task_NotifyClient_di" bpmnElement="Task_NotifyClient">
+        <dc:Bounds x="750" y="178" width="110" height="80" />
+      </bpmndi:BPMNShape>
+
       <bpmndi:BPMNShape id="Gateway_ParallelSplit_di" bpmnElement="Gateway_ParallelSplit">
-        <dc:Bounds x="750" y="193" width="50" height="50" />
+        <dc:Bounds x="900" y="193" width="50" height="50" />
       </bpmndi:BPMNShape>

       <bpmndi:BPMNShape id="Task_Cook_di" bpmnElement="Task_Cook">
-        <dc:Bounds x="850" y="100" width="100" height="80" />
+        <dc:Bounds x="1000" y="100" width="100" height="80" />
       </bpmndi:BPMNShape>

       <bpmndi:BPMNShape id="Task_FindCourier_di" bpmnElement="Task_FindCourier">
-        <dc:Bounds x="850" y="240" width="100" height="80" />
+        <dc:Bounds x="1000" y="240" width="100" height="80" />
       </bpmndi:BPMNShape>

       <bpmndi:BPMNShape id="Gateway_ParallelJoin_di" bpmnElement="Gateway_ParallelJoin">
-        <dc:Bounds x="1000" y="193" width="50" height="50" />
+        <dc:Bounds x="1150" y="193" width="50" height="50" />
       </bpmndi:BPMNShape>

       <bpmndi:BPMNShape id="Task_Deliver_di" bpmnElement="Task_Deliver">
-        <dc:Bounds x="1100" y="178" width="100" height="80" />
+        <dc:Bounds x="1250" y="178" width="100" height="80" />
       </bpmndi:BPMNShape>

       <bpmndi:BPMNShape id="EndEvent_Success_di" bpmnElement="EndEvent_Success">
-        <dc:Bounds x="1252" y="200" width="36" height="36" />
+        <dc:Bounds x="1402" y="200" width="36" height="36" />
       </bpmndi:BPMNShape>

       <bpmndi:BPMNEdge id="Flow_1_di" bpmnElement="Flow_1">
@@ -191,38 +202,42 @@
         <di:waypoint x="700" y="218" />
         <di:waypoint x="750" y="218" />
       </bpmndi:BPMNEdge>
+      <bpmndi:BPMNEdge id="Flow_5b_di" bpmnElement="Flow_5b">
+        <di:waypoint x="860" y="218" />
+        <di:waypoint x="900" y="218" />
+      </bpmndi:BPMNEdge>
       <bpmndi:BPMNEdge id="Flow_ToEndCancel_di" bpmnElement="Flow_ToEndCancel">
         <di:waypoint x="680" y="400" />
         <di:waypoint x="680" y="460" />
         <di:waypoint x="662" y="460" />
       </bpmndi:BPMNEdge>
       <bpmndi:BPMNEdge id="Flow_6_Cook_di" bpmnElement="Flow_6_Cook">
-        <di:waypoint x="775" y="193" />
-        <di:waypoint x="775" y="140" />
-        <di:waypoint x="850" y="140" />
+        <di:waypoint x="925" y="193" />
+        <di:waypoint x="925" y="140" />
+        <di:waypoint x="1000" y="140" />
       </bpmndi:BPMNEdge>
       <bpmndi:BPMNEdge id="Flow_6_Courier_di" bpmnElement="Flow_6_Courier">
-        <di:waypoint x="775" y="243" />
-        <di:waypoint x="775" y="280" />
-        <di:waypoint x="850" y="280" />
+        <di:waypoint x="925" y="243" />
+        <di:waypoint x="925" y="280" />
+        <di:waypoint x="1000" y="280" />
       </bpmndi:BPMNEdge>
       <bpmndi:BPMNEdge id="Flow_7_Cook_di" bpmnElement="Flow_7_Cook">
-        <di:waypoint x="950" y="140" />
-        <di:waypoint x="1025" y="140" />
-        <di:waypoint x="1025" y="193" />
+        <di:waypoint x="1100" y="140" />
+        <di:waypoint x="1175" y="140" />
+        <di:waypoint x="1175" y="193" />
       </bpmndi:BPMNEdge>
       <bpmndi:BPMNEdge id="Flow_7_Courier_di" bpmnElement="Flow_7_Courier">
-        <di:waypoint x="950" y="280" />
-        <di:waypoint x="1025" y="280" />
-        <di:waypoint x="1025" y="243" />
+        <di:waypoint x="1100" y="280" />
+        <di:waypoint x="1175" y="280" />
+        <di:waypoint x="1175" y="243" />
       </bpmndi:BPMNEdge>
       <bpmndi:BPMNEdge id="Flow_8_di" bpmnElement="Flow_8">
-        <di:waypoint x="1050" y="218" />
-        <di:waypoint x="1100" y="218" />
+        <di:waypoint x="1200" y="218" />
+        <di:waypoint x="1250" y="218" />
       </bpmndi:BPMNEdge>
       <bpmndi:BPMNEdge id="Flow_9_di" bpmnElement="Flow_9">
-        <di:waypoint x="1200" y="218" />
-        <di:waypoint x="1252" y="218" />
+        <di:waypoint x="1350" y="218" />
+        <di:waypoint x="1402" y="218" />
       </bpmndi:BPMNEdge>

     </bpmndi:BPMNPlane>
```

## Вывод по демонстрации

Видно, что Git точно отслеживает построчные изменения в текстовом XML-файле:
добавление новой задачи `Task_NotifyClient`, новой связи `Flow_5b` и правку
координат соседних элементов диаграммы. Это подтверждает, что `.bpmn`, как и
любой текстовый формат, хорошо версионируется и позволяет видеть детальную
историю изменений.

Для сравнения: команда `git diff` для бинарного файла `process-bpmn.png`
покажет только строку `Binary files a/lab1/diagrams/process-bpmn.png and
b/lab1/diagrams/process-bpmn.png differ` — без каких-либо деталей о том, что
именно изменилось внутри картинки.
