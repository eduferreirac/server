<template>
    <div class="sharingTabDetailsView">
        <div class="sharingTabDetailsView__header">
            <span>
                <FolderIcon :size="40" />
            </span>
            <span>
                <h1>{{ t('file_sharing', 'Edit Share Link') }}</h1>
                <small>Dummy: Important documents</small>
            </span>
        </div>
        <div class="sharingTabDetailsView__quick-permissions">
            <ul>
                <li> <span>
                        <ViewIcon />
                    </span> View only</li>
                <li> <span>
                        <EditIcon />
                    </span> Edit</li>
                <li> <span>
                        <UploadIcon />
                    </span> File drop</li>
            </ul>
        </div>
        <div class="sharingTabDetailsView__advanced-control">
            <button @click="advancedSectionAccordionExpanded = !advancedSectionAccordionExpanded">
                Advanced Settings
                <span>
                    <MenuDownIcon />
                </span>
            </button>
        </div>
        <div v-if="advancedSectionAccordionExpanded" class="sharingTabDetailsView__advanced">
            <section>
                <NcTextField :value.sync="noteToRecipient" :label="t('file_sharing', 'Note to recipient')"
                    :label-visible="true" :show-trailing-button="noteToRecipient !== ''"
                    @trailing-button-click="noteToRecipient = ''">
                </NcTextField>
                <NcCheckboxRadioSwitch :checked.sync="setPassword">{{ t('file_sharing', 'Set password') }}
                </NcCheckboxRadioSwitch>
                <NcInputField :label="t('file_sharing', 'Password')">
                </NcInputField>

                <NcCheckboxRadioSwitch :checked.sync="setExpirationDate">{{ t('file_sharing', 'Set expiration date') }}
                </NcCheckboxRadioSwitch>
                <NcInputField :value.sync="expirationDate" :label="t('file_sharing', 'Expiration date')">
                </NcInputField>
                <NcCheckboxRadioSwitch :checked.sync="hideDownload">{{ t('file_sharing', 'Hide download') }}
                </NcCheckboxRadioSwitch>
                <NcInputField :value.sync="shareLabel" :label-visible="true" :label="t('file_sharing', 'Share label')">
                </NcInputField>
            </section>
        </div>

        <div class="sharingTabDetailsView__footer">
            <a href="">
                <CloseIcon />
                Delete link
            </a>
            <div class="button-group">
                <NcButton @click="$emit('close-sharing-details')">{{ t('file_sharing', 'Cancel') }}</NcButton>
                <NcButton>{{ t('file_sharing', 'Share & copy link') }}</NcButton>
            </div>
        </div>
    </div>
</template>
  
<script>
import NcButton from '@nextcloud/vue/dist/Components/NcButton.js'
import NcInputField from '@nextcloud/vue/dist/Components/NcInputField.js'
import NcTextField from '@nextcloud/vue/dist/Components/NcTextField.js'
import NcCheckboxRadioSwitch from '@nextcloud/vue/dist/Components/NcCheckboxRadioSwitch.js'
import FolderIcon from 'vue-material-design-icons/Folder.vue'
import CloseIcon from 'vue-material-design-icons/Close.vue'
import EditIcon from 'vue-material-design-icons/Pencil.vue'
import ViewIcon from 'vue-material-design-icons/Eye.vue'
import UploadIcon from 'vue-material-design-icons/Upload.vue'
import MenuDownIcon from 'vue-material-design-icons/MenuDown.vue'

export default {
    name: 'SharingDetailsTab',
    components: {
        NcButton,
        NcInputField,
        NcTextField,
        NcCheckboxRadioSwitch,
        FolderIcon,
        CloseIcon,
        EditIcon,
        ViewIcon,
        UploadIcon,
        MenuDownIcon,
    },
    data() {
        return {
            setPassword: false,
            password: '',
            noteToRecipient: '',
            setExpirationDate: false,
            expirationDate: '',
            hideDownload: false,
            shareLabel: '',
            advancedSectionAccordionExpanded: false,
        };
    },
    methods: {
    },
    mounted() {
    }
};
</script>
  
<style lang="scss" scoped>
.sharingTabDetailsView {
    width: 96%;
    margin: 0 auto;

    &__header {
        display: flex;
        align-items: center;
        justify-content: left;
        width: 100%;
        margin-bottom: 0.2em;
        box-sizing: border-box;

        span:nth-child(1) {
            align-items: center;
            justify-content: center;
            color: var(--color-primary-element);
            padding: 0.1em;
        }

        span:nth-child(2) {
            display: flex;
            flex-direction: column;
            justify-content: left;
            align-items: flex-start;
            text-align: left;

            h1 {
                margin: 0;
                font-size: 16px;
            }

            small {
                font-size: 12px;
                margin-top: 0;
                color: rgb(65, 62, 62);
            }
        }
    }


    &__quick-permissions {
        display: flex;
        justify-content: center;
        margin-bottom: 0.2em;

        ul {
            list-style: none;
            margin: 0;
            border: 2px solid #ddd;
            text-align: left;
            width: 100%;
            box-sizing: border-box;

            li {
                padding: 0.5em;
                display: flex;
                flex-direction: row;
                border-bottom: 1px solid #ddd;

                span:nth-child(1) {
                    align-items: center;
                    justify-content: center;
                    color: var(--color-primary-element);
                    padding: 0.1em;
                }

                &:last-child {
                    border-bottom: none;
                }
            }
        }
    }

    &__advanced-control {
        button {
            display: flex;
            border: none;
            background-color: transparent;
            color: inherit;
            font: inherit;
            font-weight: bolder;
            line-height: normal;
            overflow: visible;
            text-align: inherit;
            text-transform: none;
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
            cursor: pointer;

            &:focus {
                outline: none;
            }
        }

    }

    &__advanced {
        margin-bottom: 0.5em;

        section {
            input {
                border-radius: 0 !important;
            }
        }
    }

    &__footer {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: flex-start;

        a {
            display: flex;
            align-items: center;
            color: rgb(223, 7, 7);
            text-decoration: underline;
            font-size: 16px;
        }

        .button-group {
            display: flex;
            justify-content: space-between;
            width: 100%;
            margin-top: 16px;

            button {
                flex: 1;
                margin-left: 16px;

                &:first-child {
                    margin-left: 0;
                }
            }
        }
    }
}
</style>
