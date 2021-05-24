<template>
  <div class="h-100">
    <div
      v-if="$fetchState.pending || noLogs || $fetchState.error"
      class="
        d-flex
        flex-column
        align-items-center
        justify-content-center
        h-100
        p-2
      "
    >
      <img alt="Umbrel" src="@/assets/logo.svg" class="mb-5 logo" />
      <p v-if="$fetchState.pending" class="text-muted w-75 text-center">
        Fetching debug logs...
      </p>
      <p v-else-if="noLogs" class="text-muted w-75 text-center">
        Logs not found.
      </p>
      <p v-else-if="$fetchState.error" class="text-muted w-75 text-center">
        An error occurred.
      </p>
    </div>
    <div v-else class="h-100">
      <div v-if="displayedLogs == 'main'" class="w-100 mw-100">
        <LogsDisplay :logs="splitLogs['main']" />
      </div>
      <div v-else-if="displayedLogs == 'apps'" class="w-100 mw-100">
        <LogsDisplay :logs="splitLogs['apps']" />
      </div>
      <div v-else-if="displayedLogs == 'dmesg'" class="w-100 mw-100">
        <LogsDisplay :logs="splitLogs['dmesg']" />
      </div>
      <div v-else class="p-4 w-100 mw-100">Logs not found!</div>
      <div
        class="
          p-2
          mt-auto
          fixed-bottom
          d-flex
          flex-row
          align-items-center
          justify-content-center
          no-scrollbar
          bg-dark
        "
      >
        <button
          v-if="displayedLogs !== 'main'"
          class="m-2"
          size="sm"
          variant="outline-success"
          @click="displayedLogs = 'main'"
        >
          <svg
            viewBox="0 0 16 16"
            width="1em"
            height="1em"
            focusable="false"
            role="img"
            aria-label="blank"
            xmlns="http://www.w3.org/2000/svg"
            fill="green"
            class="bi-blank mr-1 b-icon bi"
          >
            <path
              d="M8 0a.5.5 0 0 1 .5.5v.514C12.625 1.238 16 4.22 16 8c0 0 0 .5-.5.5-.149 0-.352-.145-.352-.145l-.004-.004-.025-.023a3.484 3.484 0 0 0-.555-.394A3.166 3.166 0 0 0 13 7.5c-.638 0-1.178.213-1.564.434a3.484 3.484 0 0 0-.555.394l-.025.023-.003.003s-.204.146-.353.146-.352-.145-.352-.145l-.004-.004-.025-.023a3.484 3.484 0 0 0-.555-.394 3.3 3.3 0 0 0-1.064-.39V13.5H8h.5v.039l-.005.083a2.958 2.958 0 0 1-.298 1.102 2.257 2.257 0 0 1-.763.88C7.06 15.851 6.587 16 6 16s-1.061-.148-1.434-.396a2.255 2.255 0 0 1-.763-.88 2.958 2.958 0 0 1-.302-1.185v-.025l-.001-.009v-.003s0-.002.5-.002h-.5V13a.5.5 0 0 1 1 0v.506l.003.044a1.958 1.958 0 0 0 .195.726c.095.191.23.367.423.495.19.127.466.229.879.229s.689-.102.879-.229c.193-.128.328-.304.424-.495a1.958 1.958 0 0 0 .197-.77V7.544a3.3 3.3 0 0 0-1.064.39 3.482 3.482 0 0 0-.58.417l-.004.004S5.65 8.5 5.5 8.5c-.149 0-.352-.145-.352-.145l-.004-.004a3.482 3.482 0 0 0-.58-.417A3.166 3.166 0 0 0 3 7.5c-.638 0-1.177.213-1.564.434a3.482 3.482 0 0 0-.58.417l-.004.004S.65 8.5.5 8.5C0 8.5 0 8 0 8c0-3.78 3.375-6.762 7.5-6.986V.5A.5.5 0 0 1 8 0zM6.577 2.123c-2.833.5-4.99 2.458-5.474 4.854A4.124 4.124 0 0 1 3 6.5c.806 0 1.48.25 1.962.511a9.706 9.706 0 0 1 .344-2.358c.242-.868.64-1.765 1.271-2.53zm-.615 4.93A4.16 4.16 0 0 1 8 6.5a4.16 4.16 0 0 1 2.038.553 8.688 8.688 0 0 0-.307-2.13C9.434 3.858 8.898 2.83 8 2.117c-.898.712-1.434 1.74-1.731 2.804a8.687 8.687 0 0 0-.307 2.131zm3.46-4.93c.631.765 1.03 1.662 1.272 2.53.233.833.328 1.66.344 2.358A4.14 4.14 0 0 1 13 6.5c.77 0 1.42.23 1.897.477-.484-2.396-2.641-4.355-5.474-4.854z"
            ></path>
          </svg>
          View Umbrel logs
        </button>
        <button
          v-if="displayedLogs !== 'apps'"
          class="m-2"
          size="sm"
          variant="outline-success"
          @click="displayedLogs = 'apps'"
        >
          <svg
            viewBox="0 0 16 16"
            width="1em"
            height="1em"
            focusable="false"
            role="img"
            aria-label="app"
            xmlns="http://www.w3.org/2000/svg"
            fill="currentColor"
            class="bi-app mr-1 b-icon bi"
          >
            <g>
              <path
                d="M11 2a3 3 0 0 1 3 3v6a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3V5a3 3 0 0 1 3-3h6zM5 1a4 4 0 0 0-4 4v6a4 4 0 0 0 4 4h6a4 4 0 0 0 4-4V5a4 4 0 0 0-4-4H5z"
              ></path>
            </g>
          </svg>
          View app logs
        </button>
        <button
          v-if="displayedLogs !== 'dmesg'"
          size="sm"
          variant="outline-success"
          @click="displayedLogs = 'dmesg'"
        >
          <svg
            viewBox="0 0 16 16"
            width="1em"
            height="1em"
            focusable="false"
            role="img"
            aria-label="file code"
            xmlns="http://www.w3.org/2000/svg"
            fill="currentColor"
            class="bi-file-code mr-1 b-icon bi"
          >
            <g>
              <path
                d="M6.646 5.646a.5.5 0 1 1 .708.708L5.707 8l1.647 1.646a.5.5 0 0 1-.708.708l-2-2a.5.5 0 0 1 0-.708l2-2zm2.708 0a.5.5 0 1 0-.708.708L10.293 8 8.646 9.646a.5.5 0 0 0 .708.708l2-2a.5.5 0 0 0 0-.708l-2-2z"
              ></path>
              <path
                d="M2 2a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V2zm10-1H4a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h8a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1z"
              ></path>
            </g>
          </svg>
          View dmesg logs
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
// import { BIconUmbrella, BIconApp, BIconFileCode } from 'bootstrap-icons-vue'
import AnsiUp from 'ansi_up';
import 'bootstrap/dist/css/bootstrap.min.css';

type Logs = {
  main?: string;
  dmesg?: string;
  apps?: string;
};

type SplitLogs = {
  main?: string[];
  dmesg?: string[];
  apps?: string[];
};

type LogsData = {
  logs: Logs;
  splitLogs: SplitLogs;
  displayedLogs: keyof Logs;
  noLogs: boolean;
};

export default Vue.extend({
  /* components: {
    BIconUmbrella,
    BIconApp,
    BIconFileCode,
  }, */
  data(): LogsData {
    return {
      logs: { main: '' } as Logs,
      displayedLogs: 'main',
      noLogs: false,
      splitLogs: {},
    };
  },
  async fetch() {
    this.logs = await fetch(`https://api.debug.umbrel.tech/api/read`, {
      method: 'POST',
      body: JSON.stringify({
        key: this.$nuxt.context.route.path.substring(1),
      }),
      headers: {
        'Content-Type': 'application/json',
      },
    }).then((res) => res.json());
    if (!this.logs) {
      this.noLogs = true;
    }
    const ansiUp = new AnsiUp();

    let element: keyof Logs;
    for (element in this.logs) {
      this.splitLogs[element] = ansiUp
        .ansi_to_html(this.logs[element] || 'Not found')
        .split('\n');
    }
  },
  watch: {
    '$route.query': '$fetch',
  },
});
</script>
