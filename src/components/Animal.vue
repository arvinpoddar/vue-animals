<template>
  <div class="v-animal-avatar" :style="styleVars">
    <img
      :src="getAvatar"
      :alt="avatarName"
      class="v-animal-image"
      :class="dance ? 'v-animal-dance' : ''"
    />
  </div>
</template>

<script>
import { animals, colors } from "./constants";

export default {
  name: "animal",
  props: {
    name: String,
    color: String,
    size: {
      type: String,
      default: "70px"
    },
    rounded: Boolean,
    square: Boolean,
    dance: Boolean
  },
  computed: {
    avatarName() {
      if (this.name) {
        const lower = this.name.toLowerCase();
        if (animals.includes(lower)) {
          return lower;
        }
        console.error(
          `InvalidAnimal: '${this.name}' is not a valid animal name. Using random animal instead.`
        );
      }
      return animals[(animals.length * Math.random()) << 0];
    },

    getAvatar() {
      var images = require.context("./animals/", false, /\.png$/);
      return images("./" + this.avatarName + ".png");
    },

    avatarColor() {
      if (this.color) {
        const lower = this.color.toLowerCase();
        if (lower in colors) {
          return colors[lower];
        } else if (lower === "none") {
          return "transparent";
        } else if (/^#[0-9A-F]{6}$/i.test(lower)) {
          return lower;
        } else {
          console.error(
            `InvalidColor: '${this.color}' is not a valid color. Using random color instead.`
          );
        }
      }
      const keys = Object.keys(colors);
      return colors[keys[(keys.length * Math.random()) << 0]];
    },

    avatarSize() {
      if (
        this.size.match(
          /(^\d*)(em|ex|%|px|cm|mm|in|pt|pc|ch|rem|vh|vw|vmin|vmax)/
        )
      ) {
        return this.size;
      } else {
        console.error(
          `InvalidSize: '${this.size}' is not a valid CSS width property. Using '70px' instead.`
        );
      }
      return "70px";
    },

    borderRadius() {
      if (this.rounded) {
        return "10%";
      } else if (this.square) {
        return "0px";
      }
      return "50%";
    },

    styleVars() {
      return {
        "--a-bg-color": this.avatarColor,
        "--a-size": this.avatarSize,
        "--a-border-radius": this.borderRadius
      };
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import url("./animation.css");
.v-animal-avatar {
  height: var(--a-size);
  width: var(--a-size);
  border-radius: var(--a-border-radius);
  background-color: var(--a-bg-color);
  display: flex;
  align-items: center;
  justify-content: center;
  max-height: 200px;
  max-width: 200px;
  .v-animal-image {
    width: 80%;
    height: 80%;
    user-select: none;
  }
}

.v-animal-dance {
  -webkit-animation: v-a-dance 2s infinite;
  -moz-animation: v-a-dance 2s infinite;
  animation: v-a-dance 2s infinite;
}
</style>
