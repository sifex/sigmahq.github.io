<template>
  <div class="relative">
    <div
      id="window-wrapper"
      class="left-0 top-0 flex flex-col gap-2 md:absolute md:translate-y-[-50%] lg:gap-4"
    >
      <div
        id="window"
        class="relative w-full rounded-xl p-4 text-xs md:p-8 md:pr-32 lg:text-sm"
      >
        <div class="line hidden lg:block"></div>
        <div id="window-actions" class="flex h-3 gap-2 md:h-6">
          <div class="h-3 w-3 rounded-full bg-slate-400/20"></div>
          <div class="h-3 w-3 rounded-full bg-slate-400/20"></div>
          <div class="h-3 w-3 rounded-full bg-slate-400/20"></div>
        </div>

        <div class="glow-top"></div>
        <div class="glow-bottom"></div>
        <div
          class="absolute left-0 top-6 hidden w-full text-center text-xs text-slate-400/60 md:block"
        >
          aws_root_account_usage.yml
        </div>
        <pre
          class="whitespace-pre-wrap text-wrap pt-2 md:whitespace-pre lg:pl-8"
          v-html="sigma_rule_hl"
        ></pre>
      </div>
      <div
        class="flex w-full justify-center gap-2 md:justify-start lg:justify-center"
      >
        <!--                <div class="absolute w-3 bg-[var(&#45;&#45;vp-c-brand-2)] -z-10 h-[200px] -translate-y-[50%] opacity-10"></div>-->
        <div
          class="relative inline-block rounded bg-slate-900 px-2.5 py-1.5 text-sm text-slate-300 dark:bg-[#0d0e13]"
        >
          <div class="flex gap-2">
            <div class="">
              <span class="text-[var(--vp-c-brand)]">$</span>
            </div>
            <div class="">
              <pre
                class="whitespace-pre-wrap md:whitespace-pre"
              >sigma convert <span class="text-slate-500">&#8209;t</span>&nbsp;splunk <span class="text-slate-500">&#8209;p</span>&nbsp;config.yml ...</pre>
            </div>
          </div>
        </div>
        <a
          class="relative flex w-12 items-center justify-center rounded border-2 border-sigma-400 bg-sigma-50 text-sigma-700 outline outline-2 outline-offset-2 outline-transparent transition-all hover:bg-sigma-500 hover:text-white hover:outline-sigma-500 dark:bg-slate-400/20 dark:text-white md:w-8"
          href="https://sigconverter.io/#backend=splunk&format=default&pipeline=&rule=dGl0bGU6IEFXUyBSb290IENyZWRlbnRpYWxzCmRlc2NyaXB0aW9uOiBEZXRlY3RzIEFXUyByb290IGFjY291bnQgdXNhZ2UKbG9nc291cmNlOgogICAgcHJvZHVjdDogYXdzCiAgICBzZXJ2aWNlOiBjbG91ZHRyYWlsCmRldGVjdGlvbjoKICAgIHNlbGVjdGlvbjoKICAgICAgICB1c2VySWRlbnRpdHkudHlwZTogUm9vdAogICAgZmlsdGVyOgogICAgICAgIGV2ZW50VHlwZTogQXdzU2VydmljZUV2ZW50CiAgICBjb25kaXRpb246IHNlbGVjdGlvbiBhbmQgbm90IGZpbHRlcgpmYWxzZXBvc2l0aXZlczoKICAgIC0gQVdTIFRhc2tzIFRoYXQgUmVxdWlyZSBSb290IFVzZXIgQ3JlZGVudGlhbHMKbGV2ZWw6IG1lZGl1bQ%3D%3D&pipelineYml=bmFtZTogRXhhbXBsZSBQaXBlbGluZQpwcmlvcml0eTogMzAKdHJhbnNmb3JtYXRpb25zOgotIGlkOiBzb3VyY2V0eXBlX2NvbmRpdGlvbgogIHR5cGU6IGFkZF9jb25kaXRpb24KICBjb25kaXRpb25zOgogICAgc291cmNldHlwZTogImF3czpjbG91ZHRyYWlsIgogIHJ1bGVfY29uZGl0aW9uczoKICAtIHR5cGU6IGxvZ3NvdXJjZQogICAgcHJvZHVjdDogYXdzCiAgICBzZXJ2aWNlOiBjbG91ZHRyYWls"
          target="_blank"
        >
          <ArrowUturnLeftIcon class="inline-block h-4 w-4 -scale-y-100" />
          <span class="absolute -right-1.5 -top-1.5 flex h-3 w-3">
            <span
              class="absolute inline-flex h-full w-full animate-ping rounded-full bg-sigma-400 opacity-75"
            ></span>
            <span
              class="relative inline-flex h-3 w-3 rounded-full bg-sigma-500"
            ></span>
          </span>
        </a>
      </div>
      <div
        id="splunk-output"
        class="relative w-full rounded-xl p-4 text-xs md:p-4 lg:text-sm"
      >
        <div class="glow-top splunk"></div>
        <div class="glow-bottom splunk"></div>
        <div class="flex w-full items-center gap-4">
          <div class="splunk-icon w-[32px]">
            <img
              alt=""
              class=""
              height="32"
              src="/images/backend_logos/splunk.png"
              width="32"
            />
          </div>
          <div class="gro">
            <pre
              class="whitespace-pre-wrap text-green-100 md:whitespace-pre"
              v-html="splunk_output_hl"
            ></pre>
          </div>
        </div>
      </div>

      <p
        class="hidden w-full text-center text-xs dark:text-slate-500 md:block md:text-left lg:text-center"
      >
        ... or
        <a
          class="font-medium text-[var(--vp-c-brand-1)] dark:font-normal dark:text-[var(--vp-c-brand-3)]"
          href="/docs/digging-deeper/backends#available"
          >any supported SIEM</a
        >.
      </p>

      <ThatSigmaBlur />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import ThatSigmaBlur from "../ThatSigmaBlur.vue";
import { ArrowUturnLeftIcon } from "@heroicons/vue/20/solid/index.js";
import hljs from "highlight.js/lib/core";
import yaml from "highlight.js/lib/languages/yaml";
import { default as splunk } from "../../../syntax/spl.hljs.mjs";

let code = `
title: AWS Root Credentials
description: Detects AWS root account usage
logsource:
    product: aws
    service: cloudtrail
detection:
    selection:
        userIdentity.type: Root
    filter:
        eventType: AwsServiceEvent
    condition: selection and not filter
falsepositives:
    - AWS Tasks That Require Root User Credentials
level: medium
`;

let output = `sourcetype="aws:cloudtrail" userIdentity.type="Root"\nNOT eventType="AwsServiceEvent"`;

let sigma_rule_hl = ref("");
let splunk_output_hl = ref("");

hljs.registerLanguage("yaml", yaml);
hljs.registerLanguage("spl", splunk);

sigma_rule_hl.value = hljs.highlight(code.trim(), { language: "yaml" }).value;
splunk_output_hl.value = hljs.highlight(output, { language: "spl" }).value;
</script>

<style scoped>
#window {
  background-image: linear-gradient(
    290deg,
    hsla(210, 80%, 10%, 0.9) 0%,
    hsla(210, 50%, 18%, 0.9) 100%
  );
  border: 1px solid hsl(218, 26%, 6%);
  backdrop-filter: blur(40px);
  box-shadow: inset 0 0 30px rgba(0, 0, 0, 0.2);
}

#splunk-output {
  background-image: linear-gradient(
    290deg,
    hsla(170, 100%, 8%, 0.9) 0%,
    hsla(160, 100%, 10%, 0.9) 100%
  );
  border: 1px solid hsl(140, 26%, 6%);
  backdrop-filter: blur(40px);
  box-shadow: inset 0 0 30px rgba(0, 0, 0, 0.2);
}

html.dark #window {
  background-image: linear-gradient(270deg, #12161f 0%, #101217 100%);
  border: 1px solid #1f2429;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
}

html.dark #splunk-output {
  background-image: linear-gradient(
    270deg,
    hsl(160, 27%, 10%) 0%,
    hsl(170, 18%, 8%) 100%
  );
  border: 1px solid hsl(160, 30%, 20%);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
}

.glow-top,
.glow-bottom {
  position: absolute;
  height: 1px;
  top: 0px;
  left: 15px;
  right: 15px;
  z-index: 40;
  background: linear-gradient(
    to right,
    #00b0d600 20%,
    var(--vp-c-brand-1) 50%,
    #00b0d600 80%
  );
  opacity: 0.8;
  display: none;
}

.glow-top.splunk,
.glow-bottom.splunk {
  top: -1px;
  z-index: 50;
  background: linear-gradient(
    to right,
    hsla(191, 100%, 42%, 0) 20%,
    hsl(91, 50%, 60%) 50%,
    hsla(191, 100%, 42%, 0) 80%
  );
}

html.dark .glow-top,
html.dark .glow-bottom {
  display: block;
}

.glow-top:after,
.glow-bottom:after {
  content: "";
  position: absolute;
  display: block;
  height: 10px;
  top: -5px;
  filter: blur(20px);
  left: 15px;
  right: 15px;
  z-index: 40;
  background: linear-gradient(
    to right,
    #1f2429 20%,
    var(--vp-c-brand-1) 50%,
    #1f2429 80%
  );
  opacity: 0.4;
}

.glow-top.splunk:after,
.glow-bottom.splunk:after {
  background: linear-gradient(
    to right,
    #1f2429 20%,
    hsl(91, 39%, 46%) 50%,
    #1f2429 80%
  );
}

.glow-bottom {
  top: auto;
  bottom: 0;
}

.glow-bottom.splunk {
  top: auto;
  bottom: -1px;
}

pre {
  /*white-space: nowrap;*/
  /*text-overflow: ellipsis;*/
  /*overflow: hidden;*/
}

.line {
  height: 100%;
  bottom: 0;
  top: 0;
  width: 1px;
  background: linear-gradient(
    0deg,
    hsla(218, 26%, 40%, 1) 0%,
    hsla(218, 26%, 40%, 1) 60%,
    hsla(218, 26%, 40%, 0) 86%,
    hsla(218, 26%, 40%, 0) 95%
  );
  position: absolute;
  left: 35px;
  z-index: 2;
  opacity: 0.3;
}

html.dark .line {
  background: linear-gradient(
    0deg,
    rgba(31, 36, 41, 1) 0%,
    rgba(31, 36, 41, 1) 84%,
    rgba(31, 36, 41, 0) 86%,
    rgba(31, 36, 41, 0) 95%
  );
  opacity: 0.3;
}
</style>

<style>
.hljs-attr,
.hljs-bullet {
  color: var(--vp-c-brand-1);
}

html:not(.dark) .hljs-string {
  color: #ffffff;
}

#splunk-output .hljs-literal {
  @apply text-orange-400;
}

#splunk-output .hljs-string {
  @apply text-green-300;
}
</style>
