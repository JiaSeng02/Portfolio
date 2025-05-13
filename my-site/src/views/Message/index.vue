<template>
  <div class="comment-page">
    <h1>Comments</h1>

    <div class="comment-form">
      <textarea
        v-model="newComment"
        placeholder="Write your comment here..."
        class="comment-input"
      ></textarea>
      <button @click="addComment" class="submit-btn">Post Comment</button>
    </div>

    <div class="comments-list">
      <div
        v-for="(comment, index) in comments"
        :key="index"
        class="comment-item"
      >
        <div class="comment-header">
          <span class="comment-author">User {{ index + 1 }}</span>
          <span class="comment-date">{{ formatDate(comment.date) }}</span>
        </div>
        <p class="comment-text">{{ comment.text }}</p>
        <button @click="deleteComment(index)" class="delete-btn">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CommentPage",
  data() {
    return {
      newComment: "",
      comments: [
        { text: "This is an example comment", date: new Date() },
        {
          text: "Another test comment here.",
          date: new Date(Date.now() - 86400000),
        },
      ],
    };
  },
  methods: {
    addComment() {
      if (this.newComment.trim() === "") return;

      this.comments.unshift({
        text: this.newComment,
        date: new Date(),
      });
      this.newComment = "";
    },
    deleteComment(index) {
      this.comments.splice(index, 1);
    },
    formatDate(date) {
      return date.toLocaleDateString("en-US", {
        year: "numeric",
        month: "short",
        day: "numeric",
        hour: "2-digit",
        minute: "2-digit",
      });
    },
  },
};
</script>

<style scoped>
.comment-page {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  font-family: Arial, sans-serif;
}

h1 {
  color: #2c3e50;
  text-align: center;
  margin-bottom: 2rem;
}

.comment-form {
  margin-bottom: 2rem;
  background: #f8f9fa;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.comment-input {
  width: 100%;
  min-height: 100px;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-family: inherit;
  font-size: 1rem;
  margin-bottom: 1rem;
  resize: vertical;
}

.submit-btn {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 0.8rem 1.5rem;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s;
}

.submit-btn:hover {
  background-color: #2980b9;
}

.comments-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  max-height: 400px;
  overflow-y: auto;
  padding-right: 0.5rem;
}

.comment-item {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.comment-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
  color: #7f8c8d;
}

.comment-text {
  margin: 1rem 0;
  line-height: 1.6;
  color: #333;
}

.delete-btn {
  background-color: #e74c3c;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: background-color 0.3s;
}

.delete-btn:hover {
  background-color: #c0392b;
}

@media (max-width: 600px) {
  .comment-page {
    padding: 1rem;
  }

  .comment-header {
    flex-direction: column;
    gap: 0.3rem;
  }
}
</style>
