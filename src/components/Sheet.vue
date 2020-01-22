<template>
    <div class="sheet" id="profile-sheet">
        <section>
            <div class="form-group">
                <label for="first-name">Avatar</label>
                <div class="input-group">
                    <input type="file" ref="file" accept="image/*" @change="fileUpload" multiple>
                </div>
            </div>
            <div class="form-group">
                <label for="name">Name</label>
                <div class="input-group">
                    <input type="text" class="form-control" id="name" v-model="name" />
                </div>
            </div>
            <div class="form-group">
                <label for="email">Email</label>
                <div class="input-group">
                    <input type="text" class="form-control" id="email" autoComplete="email" v-model="email" />
                </div>
            </div>
            <div class="form-group">
                <label for="role">Role</label>
                <div class="input-group">
                    <input type="text" class="form-control" id="role" v-model="role" />
                </div>
            </div>
            <div class="form-group">
                <label for="bio">Bio</label>
                <div class="input-group">
                    <input type="text" class="form-control" id="bio" v-model="bio" />
                </div>
            </div>
            <legend>Icons</legend>
            <div class="togglebox">
                <input type="checkbox" id="togglebox-example-1" v-model="icons.slack" />
                <label for="togglebox-example-1">Slack</label>
            </div>
            <div class="togglebox">
                <input type="checkbox" id="togglebox-example-2" v-model="icons.phone" />
                <label for="togglebox-example-2">Phone</label>
            </div>
            <div class="togglebox">
                <input type="checkbox" id="togglebox-example-3" v-model="icons.email" />
                <label for="togglebox-example-3">Email</label>
            </div>
            <legend>Theme</legend>
            <div class="radio">
                <input type="radio" id="radio-example-1" name="theme" value="swedbankpay" v-model="theme" />
                <label for="radio-example-1">Swedbank Pay</label>
            </div>
            <div class="radio">
                <input type="radio" id="radio-example-2" name="theme" value="payex" v-model="theme" />
                <label for="radio-example-2">PayEx</label>
            </div>
            <div class="form-group mt-5">
                <button class="btn btn-executive btn-lg" @click="createCard()">Create card</button>
            </div>
        </section>
    </div>
</template>
<script>
    export default {
        props: ["value"],
        data: () => {
            return {
                tempProfiles: [],
                avatar: 'https://picsum.photos/300/?random',
                name: 'Nicholas Cage',
                email: 'nicholas.cage@theone.com',
                role: "Some role",
                bio: 'Back in my day...',
                theme: "swedbankpay",
                tempFile: null,
                icons: {
                    slack: false,
                    phone: false,
                    email: false
                }
            }
        },
        methods: {
            fileUpload(event) {
                // eslint-disable-next-line
                console.log(event.target.files);

                this.tempFile = event.target.files[0];

                let reader = new FileReader();

                reader.addEventListener("load", function () {
                    this.avatar = reader.result;
                }.bind(this), false);

                if (this.tempFile) {
                    if (/\.(jpe?g|png|gif)$/i.test(this.tempFile.name)) {
                        reader.readAsDataURL(this.tempFile);
                    }
                }
            },
            createCard() {
                // eslint-disable-next-line
                console.log("Creating card I guess");
                this.tempProfiles = this.value || [];
                this.tempProfiles.push({
                    avatar: this.avatar,
                    name: this.name,
                    email: this.email,
                    role: this.role,
                    bio: this.bio,
                    theme: this.theme,
                    icons: {
                        slack: this.icons.slack,
                        phone: this.icons.phone,
                        email: this.icons.email
                    },
                })
                this.$emit("input", this.tempProfiles);
                window.dg.sheet.close("profile-sheet");
            }
        }
    }
</script>