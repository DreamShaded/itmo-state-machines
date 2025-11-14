<template>
  <div class="slidev-layout cover">
    <div class="cover__container">
      <div class="cover__slot">
        <slot />
      </div>
      <div class="cover__meta">
        <div class="cover__line">{{ $attrs.meetup }} · {{ $attrs.date }}</div>
        <div
          v-if="$attrs.tags && (Array.isArray($attrs.tags) ? $attrs.tags.length : true)"
          class="cover__tags"
        >
          {{ Array.isArray($attrs.tags) ? $attrs.tags.join(' · ') : $attrs.tags }}
        </div>
      </div>
    </div>
  </div>
</template>