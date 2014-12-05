Детали реализации
=================

IndexComponent используется для стандартизированного обращения к storageComponent и самому storage.

Storage есть реализация интерфейса StorageInterface.

StorageInterface призван стандартизировать обычные рутинные операции:
- createCollection - создание коллекции/индекса
- deleteCollection - удаление коллекции/индекса
Как стандартизировать параметры для создание коллекции пока что не известно(надо подумать, сравнить различные решения).

Далее надо завести абстрактный класс поведения, назовем его IndexableBehavior:
- вешается на события afterSave, afterDelete ActiveRecord
- умеет откладывать свои действия в background/task


Реализации IndexableBehavior для различных хранилищ должны собственно выполнять задачу "положи в индекс вот этот документ, а вот этот удали".
Задачу делим на следующие этапы:
- deleteDocument - удаляем старый документ
- getDocumentById - получаем существующий документ по PK основной модели
- createDocument - создаем документ
- saveDocument - сохраняем его в индекс
- saveProperties - сохраняем свойства
- saveRelations - сохраняем реляции
