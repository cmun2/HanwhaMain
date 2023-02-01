<template>
  <div class="header">
    <div class="nav-icon">
      <img src="../../assets/home.png" alt="home" />
    </div>
    <div class="nav-root">
      <ul class="nav-container">
        <li class="nav-item">
          <span>Remote</span>
        </li>
        <li class="nav-item">
          <span>User</span>
        </li>
        <li class="nav-item">
          <span>Activity List</span>
        </li>
        <li class="nav-item">
          <span>Portal Management</span>
        </li>
      </ul>
    </div>
    <div class="user-menu">
      <button class="language-choice"></button>
      <div>
        <p class="profile-menu"></p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      sampleData: "",
    };
  },
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  setup() {},
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  created() {},
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  mounted() {},
  // eslint-disable-next-line @typescript-eslint/no-empty-function
  unmounted() {},
  methods: {},
};
</script>

<style scoped lang="scss">
.header {
  width: 100%;
  background-color: #00adef;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-root {
  width: 60%;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  overflow: hidden;
}

.nav-item {
  cursor: pointer;
  position: relative;
  display: inline-block;
  color: #fff;
  font-size: 12px;
  font-weight: bold;
  padding: 8px;
}

.nav-icon {
  width: 10%;
}
.user-menu {
  width: 30%;
  display: flex;
  justify-content: center;
}

.language-choice {
  width: 200px;
  height: 30px;
  padding: 12px 20px;
  border-radius: 4px;
  box-shadow: 0 4px 10px 0 rgb(0 0 0 / 15%), 0 0 2px 0 rgb(0 0 0 / 12%);
  background-color: #fff;
  border: none;
  margin-right: 10px;
}

.profile-menu {
  width: 32px;
  height: 32px;
  margin: auto;
  cursor: pointer;
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyJpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuMy1jMDExIDY2LjE0NTY2MSwgMjAxMi8wMi8wNi0xNDo1NjoyNyAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENTNiAoV2luZG93cykiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6ODBCMENGMDg5QzFFMTFFQkI5RkE4MDk3OTRFRTFGNTgiIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6ODBCMENGMDk5QzFFMTFFQkI5RkE4MDk3OTRFRTFGNTgiPiA8eG1wTU06RGVyaXZlZEZyb20gc3RSZWY6aW5zdGFuY2VJRD0ieG1wLmlpZDo4MEIwQ0YwNjlDMUUxMUVCQjlGQTgwOTc5NEVFMUY1OCIgc3RSZWY6ZG9jdW1lbnRJRD0ieG1wLmRpZDo4MEIwQ0YwNzlDMUUxMUVCQjlGQTgwOTc5NEVFMUY1OCIvPiA8L3JkZjpEZXNjcmlwdGlvbj4gPC9yZGY6UkRGPiA8L3g6eG1wbWV0YT4gPD94cGFja2V0IGVuZD0iciI/Pr2Oo1cAAAGoSURBVHjaYvz//z/DQAImhgEGow4gxwHMQJwLxP/RcDI55jGSmAhZgPgqEKvhkL8FxNpA/IdWIbANyfIUIBYAYlEgjoOKgeSOkGQiKASIxNL/EUALi7wWkrwiseaSEgIeSMF8DYv8NagcCLjTIgoUofQmPGpgcjK0cMATKO2HRw1M7j4t0oAiCWlAmlhzSXEACJ9AsiQWiAWBmB+Ik5HEd5FiJqnlACsQXxnIcuA3EGsCcSYWuTwg1iLFcnJKwkFTGTEh1QvMSGyaOABU/lsC8UQgfgCteP5C6T9Q/B+JBqnphuphojQbev2nHDiRmwu8gHgrEn8+EG+A+vAtEH9DU88FxPzQRBoExFFIct7QiozoEGBE8sF0IGYlsbwAYRYgnodkDiMpIQDyzVcomw+IP5OZWEEh8gHK5sYSajgTyQ8kdgAFucwFif2T1ETYjRR8J6AJUgIaHYw4oo0diMWA2A2ILyDpryOnLmCExj+lAJQOmCipjKTRQoNYANKjQovKiB/aFmQDYh6kNPMZmnDfQ+sMiuoCLmwplkKA1UzG0b7hiHcAQIABAJ8Nm6HRwJftAAAAAElFTkSuQmCC);
}
</style>
