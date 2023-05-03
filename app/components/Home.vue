<template>
    <Page>
        <ActionBar>
            <Label text="Calculator 3000" class="header" />
        </ActionBar>
        
        
        <GridLayout rows="*, *, *, *, *" columns="*, *, *, *">
            <Label row="0" col="0" colSpan="4" class="label">{{ result }}</Label>
            
            <Button text="1" row="1" col="0" class="button" @tap="addToStr('1')"/>
            <Button text="2" row="1" col="1" class="button" @tap="addToStr('2')"/>
            <Button text="3" row="1" col="2" class="button" @tap="addToStr('3')"/>
            <Button text="4" row="2" col="0" class="button" @tap="addToStr('4')"/>
            <Button text="5" row="2" col="1" class="button" @tap="addToStr('5')"/>
            <Button text="6" row="2" col="2" class="button" @tap="addToStr('6')"/>
            <Button text="7" row="3" col="0" class="button" @tap="addToStr('7')"/>
            <Button text="8" row="3" col="1" class="button" @tap="addToStr('8')"/>
            <Button text="9" row="3" col="2" class="button" @tap="addToStr('9')"/>
            <Button text="0" row="4" col="0" class="button" @tap="addToStr('0')"/>
          
            <Button text="+" row="1" col="3" class="button" @tap="addToStr('+')"/>
            <Button text="*" row="2" col="3" class="button" @tap="addToStr('*')"/>
            <Button text="^" row="3" col="3" class="button" @tap="addToStr('^')"/>
            <Button text="/" row="4" col="1" class="button" @tap="addToStr('/')"/>
            <Button text="-" row="4" col="2" class="button" @tap="addToStr('-')"/>
            <Button text="=" row="4" col="3" class="button" @tap="getResult()"/>
        </GridLayout>
        
        
    </Page>
</template>

<script>
    export default {
        data () {
            return {
            result: 0,
            strForFinal: '',
            }
        },
        methods: {
            getResult: function()
            {
                this.result = eval(this.strForFinal.replace('^', '**'));     
            },
            addToStr: function(el)
            {
                this.strForFinal += el;
                this.result = this.strForFinal;
            },
            delFromStr: function()
            {
                this.strForFinal = this.strForFinal.slice(0, -1);
            }
        }
    };

</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';

    // Custom styles
    .header {
        font-size: 30pt;
        place-items: center;
        place-content: center;
    }

    .label{
        font-size: 30pt;
        place-items: right;
        place-content: right;
        place-self: right;
    }

    .button {
        font-size: 30pt;
        place-items: center;
        place-content: center;
        place-self: center;
    }
</style>
