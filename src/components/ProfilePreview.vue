<template>
  <div class="profile-preview" ref="profilePreviewElement" tabindex="-1">
    <div class="profile-preview__image">
      <img v-if="picture" :src="picture.value" alt="" />
    </div>
    <div class="profile-preview__since">Mozillian for 4 years <span class="visually-hidden">since </span><span class="profile-preview__since-start-date">July, 2016</span></div>
    <ProfileName :firstName="firstName.value" :lastName="lastName.value" :pronouns="pronouns.value"></ProfileName>
    <ProfileTitle :businessTitle="accessInformation.hris.values.businessTitle || null" :funTitle="funTitle.value"></ProfileTitle>
    <div class="hide-desktop">
      <ContactMe></ContactMe>
    </div>
    <ProfileTeamLocation :team="accessInformation.hris.values.team || null" :entity="accessInformation.hris.values.entity || null" :locationDescription="accessInformation.hris.values.locationDescription || null" :timeZone="accessInformation.hris.values.timeZone || null"></ProfileTeamLocation>

    <h2 class="visually-hidden">About</h2>
    <div class="profile__description">
      <p>{{ description.value }}</p>
    </div>
    <hr class="profile-preview__divider">
    <div class="profile-preview__buttons">
      <div class="hide-mobile">
        <ContactMe></ContactMe>
      </div>
      <router-link :to="{ name: 'Profile', params: { userId: userId.value } }" class="button button--text-only">
        View full profile
        <svg
          aria-hidden="true"
          role="presentation"
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <polyline points="9 18 15 12 9 6" />
        </svg>
      </router-link>
      <button @click="closeProfile" class="button button--icon-only button--secondary profile-preview__close">
        <span class="visually-hidden">Close profile</span>
        <svg
          aria-hidden="true"
          role="presentation"
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <line x1="18" y1="6" x2="6" y2="18" />
          <line x1="6" y1="6" x2="18" y2="18" />
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
import ContactMe from '@/components/ContactMe.vue';
import ProfileName from '@/components/ProfileName.vue';
import ProfileTitle from '@/components/ProfileTitle.vue';
import ProfileTeamLocation from '@/components/ProfileTeamLocation.vue';

export default {
  name: 'ProfilePreview',
  props: {
    type: String,
    title: String,
    content: String,
    accessInformation: Object,
    firstName: Object,
    lastName: Object,
    pronouns: Object,
    funTitle: Object,
    picture: Object,
    locationPreference: Object,
    officeLocation: Object,
    description: Object,
    created: Object,
    userId: Object,
  },
  components: {
    ContactMe,
    ProfileName,
    ProfileTitle,
    ProfileTeamLocation,
  },
  methods: {
    closeProfile() {
      this.$router.push({ name: 'Orgchart' });
      this.lastActive.focus();
      this.lastActive = document.body;
    },
  },
  mounted() {
    this.lastActive = document.activeElement;
    this.$refs.profilePreviewElement.focus();
  },
};
</script>

<style>
.profile-preview {
  background: var(--white);
  padding: 2em;
  box-shadow: var(--shadowCard);
  position: relative;
}
  .profile-preview .profile__name {
    display: block;
    margin-bottom: .5em;
  }
  .profile-preview .profile__user-name {
    margin-left: 0;
  }
  .profile-preview .profile__title,
  .profile-preview .profile__team-location {
    margin-bottom: 1.5em;
  }
  .profile-preview__image {
    width: 6.5em;
    height: 6.5em;
    border-radius: .25em;
    overflow: hidden;
    object-fit: cover;
    margin-bottom: 1em;
  }
  .profile-preview__since {
    position: relative;
    margin-bottom: 1em;
  }
    .profile-preview__since-start-date {
      position: absolute;
      left: -9999em;
    }
    .profile-preview__since:hover .profile-preview__since-start-date {
      position: absolute;
      top: -1em;
      left: 0;
    }
  .profile-preview__buttons {
    display: flex;
    align-items: start;
    justify-content: center;
  }
  @media(min-width:50em) {
    .profile-preview__buttons {
      justify-content: space-around;
    }
  }
  .profile-preview__close {
    position: absolute;
    top: 2em;
    right: 2em;
    left: auto;
    bottom: auto;
    color: var(--black);
    border-color: transparent;
    background-color: transparent;
  }
  .profile-preview__close:hover {
    background-color: transparent;
    color: var(--blue-60);
  }
  .profile-preview__divider {
    margin: 2em 0;
  }

 .modal .profile-preview {
    padding: 3em 0 0;
    box-shadow: none;
 }
 .modal .profile-preview__image {
    position: absolute;
    top: -5.25em; /* half of 6.5em picture height + 2em modal padding */
    left: 50%;
    margin-left: -3.25em; /* half of 6.5em picture height */
 }
 .modal .profile-preview__close {
    position: fixed;
    bottom: 2em;
    left: 50%;
    width: 4em;
    height: 4em;
    margin-left: -2em;
    z-index: var(--layerModal);
    background-color: var(--blue-60);
    top: auto;
    color: var(--white);
    box-shadow: 0 .125em .25em 0 var(--gray-40);
    display: flex;
    align-items: center;
  }
  .modal .profile-preview__close:hover {
    color: var(--black);
  }
  .modal .profile-preview__since {
    text-align: center;
  }
 </style>
