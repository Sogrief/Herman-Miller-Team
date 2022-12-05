<template>

  </template>

<style lang="scss" scoped>

@font-face {
    font-family: supreme;
    src: url('../../assets/fonts/SUPREME-REGULAR.OTF');
 }
@font-face {
    font-family: deserta;
    src: url('../../assets/fonts/DESERTA.OTF');
 }
@font-face {
    font-family: anurati;
    src: url('../../assets/fonts/ANURATI-REGULAR.OTF');
 }

.textBody{
    color : $bodyText;
    font-size: pxToRem(14);
    font-family: $textFontFamily;
}

.labelForm{
    color: $bodyText;
    font-size : pxTorem(12);
    font-family: $textFontFamily;
}

.liens{
    &:hover{
        color : $mainColor;
        text-decoration: underline;
    }
    
}

</style>