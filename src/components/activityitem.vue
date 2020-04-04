<template>
  <article class="post">
    <h4>{{ goal.title }}</h4>
    <div class="media">
      <div class="media-left">
        <p class="image is-32x32">
          <img src="../assets/user.png">
        </p>
      </div>
      <div class="media-content">
        <div class="content">
          <p>
            <a href="#">Filip Jerga</a> updated {{ goal.updatedAt }} &nbsp;
          </p>
        </div>
      </div>
      <div class="media-right">
        <span>Progress Bar Here</span>
      </div>
    </div>
  </article>
</template>

<script>
export default {
     props:['goal']
}
</script>

<style lang="stylus" scoped>

</style>