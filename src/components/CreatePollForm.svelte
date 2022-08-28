<style>
  form {
    width: 400px;
    margin: 0 auto;
    text-align: center;
  }

  .form-field {
    margin: 1rem 0;
  }

  input {
    margin: 0.5em 0;
    width: 100%;
    border-radius: 0.5rem;
  }

  label {
    margin: 10px auto;
    text-align: left;
  }

  .error {
    color: red;
  }
</style>

<script>
  import { createEventDispatcher } from "svelte";
  import { v4 as uuid } from "uuid";

  const dispatch = createEventDispatcher();

  let fields = { question: "", answerA: "", answerB: "" };
  let errors = { question: "", answerA: "", answerB: "" };

  function handleSubmit() {
    const poll = { ...fields, votesA: 0, votesB: 0, id: uuid() };
    dispatch("submitPoll", poll);
  }

  function validate(field, value) {
    switch (field) {
      case "question":
        if (value.length < 1) {
          errors.question = "Question must be at least 1 characters long";
        } else {
          errors.question = "";
        }
        break;
      case "answerA":
      case "answerB":
        if (value.length < 2) {
          errors[field] = "Answer must be at least 2 characters long";
        } else {
          errors[field] = "";
        }
        break;
    }
  }

  $: buttonIsDisabled =
    Object.values(errors).some(Boolean) ||
    Object.values(fields).some((v) => !Boolean(v));
</script>

<form on:submit|preventDefault={handleSubmit}>
  <div class="form-field">
    <label for="question">Poll Question:</label>
    <input
      on:blur={() => validate("question", fields.question)}
      type="text"
      id="question"
      bind:value={fields.question}
    />
    <span class="error">{errors.question}</span>
  </div>

  <div class="form-field">
    <label for="answer-a">Answer A:</label>
    <input
      on:blur={() => validate("answerA", fields.answerA)}
      type="text"
      id="answer-a"
      bind:value={fields.answerA}
    />
    <span class="error">{errors.answerA}</span>
  </div>

  <div class="form-field">
    <label for="answer-b">Answer B:</label>
    <input
      on:blur={() => validate("answerB", fields.answerB)}
      type="text"
      id="answer-b"
      bind:value={fields.answerB}
    />
    <span class="error">{errors.answerB}</span>
  </div>
  <button disabled={buttonIsDisabled}>Add Poll</button>
</form>
