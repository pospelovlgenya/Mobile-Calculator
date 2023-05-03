<template>
    <Page>
        <ActionBar>
            <Label text="Calculator"/>
            <Label>{{ result }}</Label>
        </ActionBar>

        <GridLayout rows="*, *, *, *" columns="*, *, *, *" class="info">
          <Label text="1" row="0" col="0" @tap="addToStr('1')" />
          <Label text="2" row="0" col="1" @tap="addToStr('2')"/>
          <Label text="3" row="0" col="2" @tap="addToStr('3')"/>
          <Label text="+" row="0" col="3" @tap="addToStr('+')"/>

          <Label text="4" row="1" col="0" @tap="addToStr('4')"/>
          <Label text="5" row="1" col="1" @tap="addToStr('5')"/>
          <Label text="6" row="1" col="2" @tap="addToStr('6')"/>
          <Label text="*" row="1" col="3" @tap="addToStr('*')"/>
          
          <Label text="7" row="2" col="0" @tap="addToStr('7')"/>
          <Label text="8" row="2" col="1" @tap="addToStr('8')"/>
          <Label text="9" row="2" col="2" @tap="addToStr('9')"/>
          <Label text="^" row="2" col="3" @tap="addToStr('^')"/>

          <Label text="0" row="3" col="0" @tap="addToStr('0')"/>
          <Label text="/" row="3" col="1" @tap="addToStr('/')"/>
          <Label text="-" row="3" col="2" @tap="addToStr('-')"/>
          <Label text="=" row="3" col="3" @tap="getResult()"/>
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
    .fas {
        @include colorize($color: accent);
    }

    .info {
        font-size: 20;
        place-self: center;
    }
</style>
