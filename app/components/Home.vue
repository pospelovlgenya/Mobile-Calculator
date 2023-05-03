<template>
    <Page style="background-color: #000000;">
        <ActionBar style="background-color: #FFFF00;">
            <Label text="Calculator 3000" class="header" />
        </ActionBar>
        
        
        <GridLayout rows="*, *, *, *, *, *" columns="*, *, *, *, *">
            <Label row="0" col="0" colSpan="5" class="label">{{ show }}</Label>
            
            <Button text="1" row="4" col="1" class="numButton" @tap="addToStr('1')"/>
            <Button text="2" row="4" col="2" class="numButton" @tap="addToStr('2')"/>
            <Button text="3" row="4" col="3" class="numButton" @tap="addToStr('3')"/>
            <Button text="4" row="3" col="1" class="numButton" @tap="addToStr('4')"/>
            <Button text="5" row="3" col="2" class="numButton" @tap="addToStr('5')"/>
            <Button text="6" row="3" col="3" class="numButton" @tap="addToStr('6')"/>
            <Button text="7" row="2" col="1" class="numButton" @tap="addToStr('7')"/>
            <Button text="8" row="2" col="2" class="numButton" @tap="addToStr('8')"/>
            <Button text="9" row="2" col="3" class="numButton" @tap="addToStr('9')"/>
            <Button text="0" row="5" col="2" class="numButton" @tap="addToStr('0')"/>

            
            <Button text="-(x)" row="5" col="1" class="funcButton" @tap="modStr('-', '')"/>
            <Button text="." row="5" col="3" class="funcButton" @tap="addToStr('.')"/>
          
            
            <Button text="x^y" row="2" col="0" class="funcButton" @tap="modStr('', '^')"/>
            <Button text="x^2" row="3" col="0" class="funcButton" @tap="modStr('', '^2')"/>
            <Button text="√x" row="4" col="0" class="funcButton" @tap="modStr('', '^0.5')"/>
            <Button text="^" row="5" col="0" class="funcButton" @tap="addToStr('^')"/>
            
            <Button text="C" row="1" col="0" class="funcButton" @tap="reFresh()"/>
            <Button text="BS" row="1" col="1" class="funcButton" @tap="delFromStr()"/>
            <Button text="(" row="1" col="2" class="funcButton" @tap="addToStr('(')"/>
            <Button text=")" row="1" col="3" class="funcButton" @tap="addToStr(')')"/>

            <Button text="/" row="1" col="4" class="funcButton" @tap="addToStr('/')"/>
            <Button text="*" row="2" col="4" class="funcButton" @tap="addToStr('*')"/>
            <Button text="-" row="3" col="4" class="funcButton" @tap="addToStr('-')"/>
            <Button text="+" row="4" col="4" class="funcButton" @tap="addToStr('+')"/>
            <Button text="=" row="5" col="4" class="funcButton" @tap="getResult()"/>
            

        </GridLayout>
        
        
    </Page>
</template>

<script>
import { orientation } from '@nativescript/core/application';

    export default {
        data () {
            return {
            show: ' ',
            strForFinal: '',
            }
        },
        methods: {
            getResult: function()
            {
                try {
                    this.getShow(('=' + eval(this.strForFinal.replace('^', '**').replace('/0', 'нет'))).replace('=NaN', 'Вы ошиблись').replace('=undefined', 'Вы ошиблись'));
                }
                catch {
                    this.getShow("Вы ошиблись")
                }
            },
            addToStr: function(el)
            {
                this.strForFinal += el;
                this.getShow(this.strForFinal);
            },
            modStr: function(stel, enel) {
                this.strForFinal = stel + '(' + this.strForFinal + ')' + enel;
                this.getShow(this.strForFinal);
            },
            delFromStr: function()
            {
                this.strForFinal = this.strForFinal.slice(0, -1);
                this.getShow(this.strForFinal);
            },
            reFresh: function() {
                this.strForFinal = '';
                this.getShow(this.strForFinal);
            },
            getShow: function(str) {
                let coef = orientation() == "portrait"? 1 : 2;
                let len = str.length;
                let maxLen = 23 * coef - 1;
                if (len >= maxLen) {
                    this.show = str.slice(len - maxLen, len);
                }
                else {
                    let rep = maxLen - len;
                    this.show = ' '.repeat(rep*1.2) + str;
                }
            }
        }
    };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';
    @import 'app/app.scss';
</style>
