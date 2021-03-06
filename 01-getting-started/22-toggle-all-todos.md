# TOGGLING ALL TODOS BETWEEN COMPLETE AND INCOMPLETE
# すべてのTodoの完了と未完了を切り替える

TodoMVC allows user to toggle all existing todos into either a complete or incomplete state. It uses the same checkbox that becomes checked when all todos are completed and unchecked when one or more todos remain incomplete.

TodoMVCでは、ユーザーはすべての既存のTodoを、一度に完了または未完了の状態のいずれかに切り替えることができます。そのために、すべてのTodoが完了済みになったときにチェックされ、一つまたはそれ以上のTodoが未完了のときにチェックがはずれる、同じチェックボックスを使います。

To implement this behavior update the `allAreDone` property in `js/controllers/todos_controller.js` to handle both getting and setting behavior:

この動作を実装するために、`js/controllers/todos_controller.js`の`allAreDone`プロパティを、getとsetの動作の両方を扱えるように更新します。

```javascript
// ... additional lines truncated for brevity ...
allAreDone: function (key, value) {
  if (value === undefined) {
    return !!this.get('length') && this.everyProperty('isCompleted', true);
  } else {
    this.setEach('isCompleted', value);
    this.invoke('save');
    return value;
  }
}.property('@each.isCompleted')
// ... additional lines truncated for brevity ...
```

If no `value` argument is passed this property is being used to populate the current value of the checkbox. If a `value` is passed it indicates the checkbox was used by a user and we should set the `isCompleted` property of each todo to this new value.

もしvalue引数が渡されないなら、このプロパティは、チェックボックスに現在の値を設定するために使用されます。もし、value引数が渡されるなら、チェックボックスがユーザーによって使用されたことを示しているので、各TodoのisCompletedプロパティをこの新しい値にセットします。

The count of remaining todos and completed todos used elsewhere in the template automatically re-render for us if necessary.

必要であれば、テンプレートの中で使われている残りのTodoと完了済みTodoのカウントが、自動的に再レンダリングされます。

Reload your web browser to ensure that there are no errors and the behavior described above occurs. 

ウェブブラウザーをリロードして、何もエラーが起きないことと、上述の動作が行われることを確認してください。

### Live Preview
### ライブ・プレビュー
<a class="jsbin-embed" href="http://jsbin.com/AViZATE/1/embed?live">Ember.js • TodoMVC</a><script src="http://static.jsbin.com/js/embed.js"></script>

### Additional Resources
### 追加リソース

  * [Changes in this step in `diff` format](https://github.com/emberjs/quickstart-code-sample/commit/47b289bb9f669edaa39abd971f5e884142988663)
  * [Ember.Checkbox API documentation](/api/classes/Ember.Checkbox.html)
  * [Computed Properties Guide](/guides/object-model/computed-properties/)

(The original document’s commit SHA1: 077fc1fa005dabeb1a760bf34a2454f852021189)