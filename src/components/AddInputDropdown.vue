<template>
<ul id='add-input-dropdown-1' class='dropdown-content'>
    <li v-for="(btn, index) in data" :key="index"><a :class="btn.class" class="bold" :href="btn.href" @click="btn.onclick">{{ btn.label }}</a></li>
</ul>
</template>

<script>
export default {
    name: 'add-input-dropdown',
    data(){
        return {
            data: [
                {
                    label: 'Video File',
                    onclick(){
                        window.$store.dispatch('loadFile', {
                            fileType: 'video/*',
                            isText: false
                        }).then(file => {
                            const fr = new window.FileReader();
                            fr.onload = () => {
                                let refinedFile = fr.result;
                                window.$store.commit('addInputSource', {
                                name: file.name,
                                id: Math.random(),
                                type: 'video file',
                                file,
                                data: refinedFile,
                                position: 0
                            })
                            }
                            fr.readAsDataURL(file);
                        }).catch(e => window.M.toast({
              html: e,
              classes: 'bold red rounded'
            }))
                    }
                },
                {
                    label: 'Audio File',
                    onclick(){
                        window.$store.dispatch('loadFile', {
                            fileType: 'audio/*, video/*',
                            isText: false
                        }).then(file => {
                            const fr = new window.FileReader();
                            fr.onload = () => {
                                let refinedFile = fr.result;
                                window.$store.commit('addInputSource', {
                                name: file.name,
                                id: Math.random(),
                                type: 'audio file',
                                file,
                                data: refinedFile,
                                position: 0
                            })
                            }
                            fr.readAsDataURL(file);
                        }).catch(e => window.M.toast({
              html: e,
              classes: 'bold red rounded'
            }))
                    }
                },
                {
                    label: 'Live Video Input',
                    onclick(){
                    },
                    href: '#select-camera-modal',
                    class: 'modal-trigger'
                },
                {
                    label: 'Live Audio Input',
                    onclick(){},
                    href: '#select-microphone-modal',
                    class: 'modal-trigger'
                },
                {
                    label: 'Remote Video Input',
                    onclick(){}
                },
                {
                    label: 'Remote Audio input',
                    onclick(){}
                },
                {
                    label: 'Image File',
                    onclick(){}
                },
                {
                    label: 'Image from URL',
                    onclick(){}
                },
                {
                    label: 'Desktop Capture',
                    onclick(){
                        window.navigator.mediaDevices.getDisplayMedia({
                            video: {
                                cursor: 'motion'
                            },
                            audio: true
                        })
                        window.$store.commit('addInputSource', {
                                name: 'Desktop Capture',
                                id: Math.random(),
                                type: 'desktop capture',
                                data: '',
                                position: 0
                            })
                    }
                },
                {
                    label: 'Layout Template',
                    onclick(){}
                }
            ]
        };
    }
}
</script>

<style>

</style>