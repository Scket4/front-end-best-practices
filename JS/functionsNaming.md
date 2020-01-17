1. **Все имена функций, за редкими исключениями (например, следование уже устоявшемуся соглашению в рамках какой-нибудь библиотеки), должны начинаться с глаголов**;

2. **Функции высшего порядка, возвращающие функции, следует именовать по шаблону make + .\* + отглагольное существительное, где .\* — опциональный, синтаксически корректный набор слов уточняющий предназначение функции**.

    Пример: `makeButtonClickHandler`.

3. **Обработчики событий** (под событиями понимаются не только DOM-события, но и какие-то абстрактные события, которые обрабатываются с помощью коллбэков, вроде `onClose` модального окна или `onLogin` формы логина):
   * **Пропсы React-компоненты, относящиеся к обработке событий, должны именоваться по шаблону `onEventName`, где `EventName` — имя обрабатываемого события**;
   * **Обработчики событий для БЭМ-элементов, а также для компонент, вложенных в БЭМ-элементы, именуются по шаблону `handleElementNameEventName`, где `ElementName` - имя БЭМ-элемента**.

      Примеры:
      ```
      <button className="block__cancel-button" onClick={this.handleCancelButtonClick} />
      <div className="block__first-name-input">
        <Input onChange={this.handleFirstNameInputChange} />
      </div>
      ```
      **Если компонента не вложена в БЭМ-элемент, то `ElementName` в данном случае стоит выбирать по смыслу, исходя из контекста** (причем, поскольку БЭМ-элементы именуются по похожему принципу, то и БЭМ-элемент в данном случае назывался бы, скорее всего, так же):
      ```
      <div className="block">
        <Button onClick={this.handleCancelButtonClick} />
        <Input onChange={this.handleFirstNameInputChange} />
      </div>
      ```

      Обоснование: именуя колбэки по такому шаблону, мы не будем тратить время на придумывание имени и всегда можем понять предназначение колбэка лишь посмотрев на его имя.

      **Примечание**: в случаях, когда тело обработчика используется где-то ещё, то его следует выносить в отдельную функцию: например, обработчик `handleButtonClick`, выводящий список итемов, может передаваться только в пропс `onClick` БЭМ-элемента "button"; если же требуется вывести список итемов еще в каких-то других случаях, то следует сделать следующим образом:
      ```
      handleButtonClick() {
        showItems();
      }

      showItems() {
        ...
      }