<template>
  <div class="error-codes">
    <p>
    <input type="text" id="error-code-search" name="filter" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false" placeholder="Search error codes for..." :value="search" @input="updateSearch"/>
    </p>
    <div id="error-code-count">Found <b>{{ resultCount }}</b> matches</div>
    <div class="error-code" v-for="oktaError in filteredErrorCodes" :key="oktaError.errorCode">
      <h4 :id="oktaError.errorCode">
        {{oktaError.title}}
        <a :href="'#'+oktaError.errorCode" aria-hidden="true" class="header-anchor header-link"><i class="fa fa-link"></i></a>
      </h4>
      <p class="error-code-description" v-if="oktaError.errorSummary">{{ oktaError.errorSummary}}</p>
      <p class="error-code-description" v-else>No Description</p>
      <pre >
        <code class="language-json">
{ 
  "errorCode": "{{oktaError.errorCode}}", 
  "errorSummary": "{{oktaError.errorSummary}}", 
  "errorLink": "{{oktaError.errorCode}}", 
  "errorId": "{UniqueErrorId}", 
  "errorCauses": [] 
}
        </code>
      </pre>

      <div class="error-code-tags">
        <code class="error-code-tag world" >{{ oktaError.statusCode }}</code>
        <code class="error-code-tag" >{{ oktaError.errorCode }}</code>
      </div>
      <div class="error-code-release">
        Since: <a href="/docs/release-notes/">2019.10.2</a>
      </div>
    </div>
  </div>
</template>

<script>
  import errorCodes from './../../vuepress-site/data/error-codes.json'
  import _ from 'lodash'

  export default {
    created() {
      this.errorCodes = errorCodes
    },
    data() {
      return {
        search: this.$route.query.q || ''
      }
    },
    computed: {
      filteredErrorCodes: function() {
        if( !this.search ) {
          return this.errorCodes.errors
        }

        return this.errorCodes.errors.filter((oktaError) => {
          return oktaError.errorCode.includes(this.search)
          || oktaError.statusCode.toString().includes(this.search)
          || oktaError.title.toLowerCase().includes(this.search.toLowerCase());
        });
      },

      resultCount() {
        return  this.filteredErrorCodes.length
      }
    },
    watch: {
      search() {
        this.addHistory()
      },
      release() {
        this.addHistory()
      }      
    },
    methods: {
      updateSearch: _.debounce(function(e) {
        this.search = e.target.value
      }, 100),
      addHistory() {
        if (history.pushState) {
          if (this.search) {
            history.pushState(null, '', '?q=' + encodeURI(this.search))
          } else if (this.httpStatus) {
            history.pushState(null, '', '?httpStatus=' + encodeURI(this.httpStatus))
          } else {
            history.pushState(null, '', this.$route.path)
          }
        }
      }
    }
  }
</script>

<style scoped lang="scss">
  .error-codes {
    .PageContent-main {
      padding-right: 0;
    }

    #error-code-search {
      width: 100%;
      border: 2px solid #d2d2d6;
    }

    #error-code-search::placeholder {
      color: #d2d2d6;
    }

    #error-code-release {
      margin-top: 1em;
    }

    #error-code-count {
      margin-top: -1em;
      margin-left: 0.3em;
      color: #888888;
      font-size: 0.9em;
    }

    .error-code {
      h4 {
        margin: 25px 0 0;
        padding: 6px 10px;
        clear: left;
        overflow: hidden;
        border-left: 3px solid #007dc1;
        color: #007dc1;
        text-overflow: ellipsis;
        white-space: nowrap;
      }

      h4::before {
        content: '\f071';
        margin-right: 8px;
        font-family: fontawesome;
      }

      pre {
        padding: 5px 0px;
        margin: 0px;

      }

      .error-code-mappings {
        margin: -1em 0;
        padding: 10px 15px;
        color: #888888;
        font-size: 0.9em;
      }

      .error-code-description {
        margin-top: 10px;
        margin-bottom: 5px;
      }

      .error-code-tag::before {
        content: '\f02b';
        padding: 2px 4px;
        font-family: fontawesome;
      }

      .error-code-tag.world::before {
        content: '\f0ac';
        padding: 2px 4px;
        font-family: fontawesome;
      }

      .error-code-tag {
        display: block;
        margin: 2px;
        padding: 1px 3px;
        float: left;
        border-radius: 3px;
        background-color: #ffffff;
        font-size: 0.7em;
      }

      .error-code-release {
        clear: both;
        opacity: 0.7;
        font-size: 0.8em;
      }
    }
  }
</style>
