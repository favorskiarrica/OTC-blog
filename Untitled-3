const form = document.getElementById("postForm");
const messageBox = document.getElementById("messageBox");
const messageList = document.getElementById("messageList");

// 1. Load messages from localStorage, or start fresh
let messages = [];
const saved = localStorage.getItem("anonMessages");
if (saved) {
  messages = JSON.parse(saved);
}

// 2. Function to save messages to localStorage
function saveMessages() {
  localStorage.setItem("anonMessages", JSON.stringify(messages));
}

// 3. Render all messages and comments with forms
function renderMessages() {
  messageList.innerHTML = "";
  messages.forEach((msg, idx) => {
    const li = document.createElement("li");
    // Message text
    const mainMsg = document.createElement("div");
    mainMsg.textContent = msg.text;
    li.appendChild(mainMsg);

    // Comments list
    const commentList = document.createElement("ul");
    commentList.style.marginLeft = "20px";
    msg.comments.forEach(comment => {
      const commentLi = document.createElement("li");
      commentLi.textContent = comment;
      commentList.appendChild(commentLi);
    });
    li.appendChild(commentList);

    // Comment input and button
    const commentForm = document.createElement("form");
    commentForm.style.display = "flex";
    commentForm.style.marginTop = "6px";

    const commentInput = document.createElement("input");
    commentInput.type = "text";
    commentInput.placeholder = "Leave a comment...";
    commentInput.required = true;
    commentInput.style.flex = "1";

    const commentBtn = document.createElement("button");
    commentBtn.textContent = "Comment";
    commentBtn.type = "submit";

    commentForm.appendChild(commentInput);
    commentForm.appendChild(commentBtn);

    // Handle adding a comment
    commentForm.addEventListener("submit", function(e) {
      e.preventDefault();
      const commentText = commentInput.value.trim();
      if (commentText.length > 0) {
        messages[idx].comments.push(commentText);
        saveMessages(); // save after comment
        renderMessages();
      }
    });

    li.appendChild(commentForm);

    messageList.appendChild(li);
  });
}

// 4. Add new message on submit
form.addEventListener("submit", function(event) {
  event.preventDefault();
  const text = messageBox.value.trim();
  if (text.length > 0) {
    messages.push({ text: text, comments: [] });
    saveMessages(); // save after new message
    renderMessages();
    messageBox.value = "";
  }
});

// 5. Initial render on page load
renderMessages();
