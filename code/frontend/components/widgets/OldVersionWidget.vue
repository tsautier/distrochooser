<!--
distrochooser
Copyright (C) 2014-2026 Christoph Müller <distrochooser@chmr.eu>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
-->
<template>
    <div :class="'col alert alert-info'" v-if="oldVersionLink && wasMigrated">
        <b class="fs-4 mb-3 d-block">
            <span class="me-1">v5</span>
            <Icon name="ion:airplane-outline" class="align-middle me-1" />
            <span class="me-1">v6: Boarding complete</span>
        </b>
        <p class="fw-bold mb-0 mt-1">
            <LanguageTranslation translation-key="old-version-migrated-fallback-alert" />
        </p>
        <p class="mb-0 mt-2">
            <LanguageTranslation translation-key="old-version-alert" />:
            <a target="_blank" :href="oldVersionLink">{{ oldVersionLink }}</a>
        </p>
    </div>
</template>
<script setup lang="ts">
import { computed } from 'vue';
import { useRoute } from 'vue-router';
import { useSessionStore } from '../../states/session';

const sessionStore = useSessionStore()

const router = useRoute();
const resultId: string | null = (router.params.resultId as string) ?? null;
const wasMigrated = computed(() => sessionStore.session && sessionStore.session.isOriginImported)
const oldVersionLink = computed(() => sessionStore.session.previousVersionUrl ? sessionStore.session.previousVersionUrl + "/" + sessionStore.session.languageCode + "/" + resultId : null)
</script>