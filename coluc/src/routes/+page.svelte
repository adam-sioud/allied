<script>
    import "@friendofsvelte/tipex/styles/Tipex.css";
    import "@friendofsvelte/tipex/styles/ProseMirror.css";
    import "@friendofsvelte/tipex/styles/Controls.css";
    import "@friendofsvelte/tipex/styles/EditLink.css";
    import "@friendofsvelte/tipex/styles/CodeBlock.css";

    import { Chat } from '@ai-sdk/svelte';
    import {Tipex} from '@friendofsvelte/tipex';

    let body = `<p> The Context Pad</p>`;
    const chat = new Chat(); 

  </script>
  
  <main>

    <Tipex {body} controls floating focal
    style="margin-top: 1rem; margin-bottom: 0;" 
    class="h-[20vh] border border-neutral-200"/>
    <ul>
      {#each chat.messages as message, messageIndex (messageIndex)}
        <li>
          <div>{message.role}</div>
          <div>
            {#each message.parts as part, partIndex (partIndex)}
              {#if part.type === 'text'}
                <div>{part.text}</div>
              {/if}
            {/each}
          </div>
        </li>
      {/each}
    </ul>
    <form onsubmit={chat.handleSubmit}>
      <input bind:value={chat.input} />
      <button type="submit">Send</button>
    </form>
  </main>