let tasks = JSON.parse(localStorage.getItem("auditTasks")) || [];

function saveTasks() {
  localStorage.setItem("auditTasks", JSON.stringify(tasks));
}

function addTask() {
  const name = document.getElementById("taskName").value.trim();
  const deadline = document.getElementById("deadline").value;

  if (!name) {
    alert("Введите название задачи");
    return;
  }

  tasks.push({
    id: Date.now(),
    name: name,
    deadline: deadline,
    status: "Новая"
  });

  document.getElementById("taskName").value = "";
  document.getElementById("deadline").value = "";

  saveTasks();
  renderTasks();
}

function changeStatus(id) {
  const task = tasks.find(t => t.id === id);

  if (task.status === "Новая") {
    task.status = "В работе";
  } else if (task.status === "В работе") {
    task.status = "Выполнена";
  } else {
    task.status = "Новая";
  }

  saveTasks();
  renderTasks();
}

function deleteTask(id) {
  tasks = tasks.filter(t => t.id !== id);
  saveTasks();
  renderTasks();
}

function renderTasks() {
  const container = document.getElementById("tasks");

  container.innerHTML = "";

  tasks.forEach(task => {
    const overdue = task.deadline &&
      new Date(task.deadline + "T00:00:00") < new Date(new Date().toDateString()) &&
      task.status !== "Выполнена";

    const div = document.createElement("div");
    div.className = "task";

    div.innerHTML = `
      <strong>${escapeHTML(task.name)}</strong>
      <p>Срок: ${task.deadline || "Не указан"}</p>
      <p>Статус: ${task.status}</p>
      ${overdue ? "<p style='color:red'>⚠ Просрочено</p>" : ""}
      <button onclick="changeStatus(${task.id})">Изменить статус</button>
      <button onclick="deleteTask(${task.id})">Удалить</button>
    `;

    container.appendChild(div);
  });

  document.getElementById("total").textContent = tasks.length;
  document.getElementById("done").textContent =
    tasks.filter(t => t.status === "Выполнена").length;
  document.getElementById("progress").textContent =
    tasks.filter(t => t.status === "В работе").length;
}

function escapeHTML(value) {
  return String(value).replace(/[&<>"']/g, char => ({
    "&": "&amp;",
    "<": "&lt;",
    ">": "&gt;",
    '"': "&quot;",
    "'": "&#039;"
  })[char]);
}

renderTasks();
