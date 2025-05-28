# Todo List :

# Command to create todo list database:
use todo_db

switched to db todo_db

## Adding 10 Todo list:
db["todolist"].find()
db.todos.insertMany([
  { task: "Buy Cloths", completed: false },
  { task: "Finish task", completed: false },
  { task: "Call mom", completed: true },
  { task: "Clean room", completed: false },
  { task: "Pay electricity bill", completed: true },
  { task: "Read a book", completed: false },
  { task: "Go to Gym", completed: true },
  { task: "Attend meeting", completed: false },
  { task: "Take a Bath", completed: false },
  { task: "Wash Cloths", completed: true }
])


{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('683737678143f7410060239b'),
    '1': ObjectId('683737678143f7410060239c'),
    '2': ObjectId('683737678143f7410060239d'),
    '3': ObjectId('683737678143f7410060239e'),
    '4': ObjectId('683737678143f7410060239f'),
    '5': ObjectId('683737678143f741006023a0'),
    '6': ObjectId('683737678143f741006023a1'),
    '7': ObjectId('683737678143f741006023a2'),
    '8': ObjectId('683737678143f741006023a3'),
    '9': ObjectId('683737678143f741006023a4')
  }
}

## Command for seeing List content:
db.todos.find().pretty()
# Output:
{
  _id: ObjectId('683737678143f7410060239b'),
  task: 'Buy Cloths',
  completed: false
}
{
  _id: ObjectId('683737678143f7410060239c'),
  task: 'Finish task',
  completed: false
}
{
  _id: ObjectId('683737678143f7410060239d'),
  task: 'Call mom',
  completed: true
}
{
  _id: ObjectId('683737678143f7410060239e'),
  task: 'Clean room',
  completed: false
}
{
  _id: ObjectId('683737678143f7410060239f'),
  task: 'Pay electricity bill',
  completed: true
}
{
  _id: ObjectId('683737678143f741006023a0'),
  task: 'Read a book',
  completed: false
}
{
  _id: ObjectId('683737678143f741006023a1'),
  task: 'Go to Gym',
  completed: true
}
{
  _id: ObjectId('683737678143f741006023a2'),
  task: 'Attend meeting',
  completed: false
}
{
  _id: ObjectId('683737678143f741006023a3'),
  task: 'Take a Bath',
  completed: false
}
{
  _id: ObjectId('683737678143f741006023a4'),
  task: 'Wash Cloths',
  completed: true
}

## Command to make Status false by default:
function addTodo(taskName) {
  db.todolist.insertOne({ task: taskName, completed: false });
}
[Function: addTodo]
addTodo("Go for a walk")
db.todolist.find({ completed: false }).pretty()


{
  _id: ObjectId('683738558143f741006023a5'),
  task: 'Go for a walk',
  completed: false
}

## Command to Update the status field from false to true for a specific task using Object ID:
db.todolist.updateOne(
  { _id: ObjectId("683738558143f741006023a5") },
  { $set: { completed: true } }
)

{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

 ## Command to Verify the update:
db.todolist.findOne({ _id: ObjectId("683738558143f741006023a5") })

{
  _id: ObjectId('683738558143f741006023a5'),
  task: 'Go for a walk',
  completed: true
}

## Command to setting up created and updated record:
db.todolist.updateMany(
  {
    _id: { 
      $in: [
        ObjectId('683737678143f7410060239b'),
        ObjectId('683737678143f7410060239c'),
        ObjectId('683737678143f7410060239d'),
        ObjectId('683737678143f7410060239e'),
        ObjectId('683737678143f7410060239f'),
        ObjectId('683737678143f741006023a0'),
        ObjectId('683737678143f741006023a1'),
        ObjectId('683737678143f741006023a2'),
        ObjectId('683737678143f741006023a3'),
        ObjectId('683737678143f741006023a4'),
        ObjectId('683738558143f741006023a5')
      ]
    }
  },
  {
    $set: {
      created: new Date(),
      updated: new Date()
    }
  }
)

{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

## Command to Count all Tasks
>db.tasks.countDocuments()
<11
