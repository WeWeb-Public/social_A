<template>
    <div class="social_A">
        <!-- wwManager:start -->
        <wwSectionEditMenu v-bind:sectionCtrl="sectionCtrl"></wwSectionEditMenu>
        <!-- wwManager:end -->
        <wwObject class="background" v-bind:ww-object="section.data.background" ww-category="background"></wwObject>
        <div class="container">
            <div class="row text-center social-blocks-container">
                <div class="block">
                    <div class="social-block" v-for="link in section.data.links" :key="link.uniqueId">
                        <div class="social-icon-container">
                            <wwObject class="social-icon" v-bind:ww-object="link.icon" ww-category="icon"></wwObject>
                        </div>
                        <wwObject class="social-text" v-bind:ww-object="link.text"></wwObject>
                        <!-- wwManager:start -->
                        <div v-show="editMode" class="edit-button-top-left" @click="removeLink(link)">
                            <i class="wwi wwi-delete" aria-hidden="true"></i>
                        </div>
                        <!-- wwManager:end -->
                    </div>
                    <!-- wwManager:start -->
                    <div v-show="editMode" class="add-link-container">
                        <div class="add-link" @click="addLink()">
                            <i class="wwi wwi-add" aria-hidden="true"></i>
                        </div>
                    </div>
                    <!-- wwManager:end -->
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "__COMPONENT_NAME__",
    props: {
        sectionCtrl: Object
    },
    data() {
        return {}
    },
    computed: {
        section() {
            return this.sectionCtrl.get();
        },
        // wwManager:start
        editMode() {
            return this.sectionCtrl.getEditMode() == 'CONTENT'
        }
        // wwManager:end
    },
    created() {
        //Initialize section data
        this.section.data = this.section.data || {};

        //Initialize background
        if (!this.section.data.background) {
            this.section.data.background = wwLib.wwObject.getDefault({ type: 'ww-color' });
        }
        //Initialize links
        if (!this.section.data.links) {
            this.section.data.links = [this.getNewLink(), this.getNewLink(), this.getNewLink()];
        }
        this.sectionCtrl.update(this.section);
    },
    methods: {
        getNewLink() {
            return {
                icon: wwLib.wwObject.getDefault({ type: 'ww-icon' }),
                text: wwLib.wwObject.getDefault({ type: 'ww-text' })
            }
        },
        // wwManager:start
        removeLink(link) {
            this.section.data.links.splice(this.section.data.links.indexOf(link), 1);
            this.sectionCtrl.update(this.section);
        },
        addLink() {
            this.section.data.links.push(this.getNewLink());
            this.sectionCtrl.update(this.section);
        }
        // wwManager:end
    }
};
</script>

<style scoped>
.social_A {
    position: relative;
    overflow: hidden;
    padding: 40px 0 30px 0;
}

.social_A .background {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
}

.social_A .social-icon-container {
    width: 100%;
    text-align: center;
    position: relative;
    margin-bottom: 5px;
}

.social_A .social-text {
    margin-bottom: 20px;
}

.social_A .social-icon {
    position: relative;
    font-size: 32px;
}

.social_A .social-block {
    display: inline-block;
    width: 50%;
    position: relative;
}

.social_A .row {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -15px;
    margin-left: -15px;
}

.social_A .block {
    position: relative;
    width: 100%;
    min-height: 1px;
    padding-right: 15px;
    padding-left: 15px;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
}

.social_A .text-center {
    text-align: center;
}

.social_A .social-icon-container {
    display: flex;
    justify-content: center;
}

.social_A .edit-button-top-left {
    position: absolute;
    left: -2px;
    top: -17px;
    width: 26px;
    height: 26px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 100%;
    text-align: center;
    font-size: 18px;
    line-height: 36px;
    cursor: pointer;
    pointer-events: all;
    z-index: 3;
    color: white;
    background-color: #E73055;
    background: linear-gradient(to right, #E73055 0%, rgb(175, 33, 61) 100%);
}

.social_A .add-link-container {
    width: 100%;
    display: flex;
    justify-content: center;
}

.social_A .add-link {
  color: white;
  cursor: pointer;
  pointer-events: all;
  font-size: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 100%;
  background-color: #1763A9;
  background: linear-gradient(to right, #1763A9 0%, #2E85C2 100%);
}

@media (min-width: 768px) {
    .social_A .social-block {
        width: 25%;
    }
}

@media (min-width: 992px) {
    .social_A .social-block {
        width: 20%;
    }
}

@media (min-width: 1200px) {
    .social_A .social-block {
        width: 16.66666%;
    }
}
</style>
