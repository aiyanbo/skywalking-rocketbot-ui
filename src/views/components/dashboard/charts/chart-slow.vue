/**
 * Licensed to the Apache Software Foundation (ASF) under one or more
 * contributor license agreements.  See the NOTICE file distributed with
 * this work for additional information regarding copyright ownership.
 * The ASF licenses this file to You under the Apache License, Version 2.0
 * (the "License"); you may not use this file except in compliance with
 * the License.  You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

<template>
  <div style="overflow: auto;height: 100%;" class="scroll_hide">
    <div class="rk-chart-slow clear">
      <div class="rk-chart-slow-i" v-for="(i, index) in data" :key="index">
        <svg class="icon vm r grey link-hover cp" @click="handleClick(i.label)">
          <use xlink:href="#review-list"></use>
        </svg>
        <div class="mb-5 ell" v-tooltip:top.ellipsis="i.label || ''">
          <span class="calls sm mr-10">{{i.value}} ms</span>
          <span class="cp link-hover"  @click="appChange(i)">{{i.label}}</span>
        </div>
        <RkProgress :precent="i.value/maxValue*100" color="#bf99f8"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';
import copy from '@/utils/copy';


@Component({})
export default class RkTopSlow extends Vue {
  @Prop() private data!: any;
  @Prop() private intervalTime!: any;
  private appChange(i: any) {
    const temp = { key: `${i.key}`, label: i.label };
  }
  get maxValue() {
    const temp: number[] = this.data.map((i: any) => i.value);
    return Math.max.apply(null, temp);
  }
  private handleClick(i: any) {
    copy(i);
  }
}
</script>
<style lang="scss">
.rk-chart-slow{
  height: 100%;
  .calls{
    padding: 0 5px;
    display: inline-block;
    background-color: #40454e;
    color: #eee;
    border-radius: 4px;
  }
}
.rk-chart-slow-i{
  padding: 6px 0;
}
</style>
