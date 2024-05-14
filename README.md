# Criando-um-App-Flutter-com-Gerenciamento-de-Estado-e-Reatividade

Vamos falar sobre a criação de um app Flutter com foco em gerenciamento de estado e reatividade, utilizando o exemplo de um app de lista de tarefas. Abordaremos o uso de três soluções populares: Provider, MobX e Get.

**Provider** é uma ferramenta recomendada pela equipe do Flutter para gerenciamento de estado simples e eficaz. Ele funciona com o conceito de InheritedWidget para disponibilizar dados para os widgets que necessitam.

**MobX** é uma biblioteca poderosa que utiliza observáveis para reagir a mudanças de estado. Com MobX, você define seus estados como observáveis e constrói ações que os modificam. Quando um estado observável muda, o MobX reage atualizando automaticamente os widgets que dependem desse estado.

**Get** é um micro-framework que oferece uma solução de gerenciamento de estado, navegação, gerenciamento de dependência e outras funcionalidades. Ele é conhecido por sua simplicidade e eficiência, permitindo que você gerencie o estado de maneira reativa com menos código.

Aqui está um exemplo de como você pode estruturar seu app de lista de tarefas em módulos, utilizando o Provider:

```dart
// main.dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'task_model.dart';
import 'task_list.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => TaskModel(),
      child: MaterialApp(
        title: 'Lista de Tarefas',
        home: TaskList(),
      ),
    );
  }
}

// task_model.dart
import 'package:flutter/foundation.dart';

class TaskModel with ChangeNotifier {
  List<String> _tasks = [];

  List<String> get tasks => _tasks;

  void addTask(String task) {
    _tasks.add(task);
    notifyListeners();
  }

  void removeTask(int index) {
    _tasks.removeAt(index);
    notifyListeners();
  }
}

// task_list.dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'task_model.dart';

class TaskList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Lista de Tarefas'),
      ),
      body: Consumer<TaskModel>(
        builder: (context, taskModel, child) {
          return ListView.builder(
            itemCount: taskModel.tasks.length,
            itemBuilder: (context, index) {
              return ListTile(
                title: Text(taskModel.tasks[index]),
                trailing: IconButton(
                  icon: Icon(Icons.delete),
                  onPressed: () {
                    taskModel.removeTask(index);
                  },
                ),
              );
            },
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Adicionar nova tarefa
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

Este é um exemplo básico de como você pode estruturar seu app Flutter com o Provider. Para MobX e Get, a estrutura seria similar, mas com suas respectivas sintaxes e métodos de gerenciamento de estado. Lembre-se de modularizar seu código para manter a organização e facilitar a manutenção. Espero que este exemplo ajude a dar um ponto de partida para o seu projeto.
