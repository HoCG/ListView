<template>
    <div id="app">

        <div id="Organozations" ref="mydiv">
            <ul class="tab-wrap">
                <li class="">
                    <a href="#tabs-1">기준시점</a>
                </li>
                <li class="">
                    <a href="#tabs-2">비교시점</a>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import Organizations_of_local from './assets/Organizations.json';
    import axios from 'axios'

    export default {
        name: 'App',
        components: {},
        data() {
            return {OrganizationsData: [], PersonnalsData: [], JsonKeyData: [], NewData: '', firstcheck: true}
        },
        created() {
            //서버 통신
            axios
                .get(
                    'https://8vxu0grpsd.execute-api.ap-northeast-2.amazonaws.com/ifm/api/ext/panpac' +
                    'ific/EIS_MONTH_TREE?tenantKey=panpacific&locale=ko_US&userToken=3b4b963a-929d-' +
                    '4235-9ab6-2048a98c4859&compareYmd=2020.08&orgCd=10111&empNm=%EC%B5%9C%EC%84%B8' +
                    '%ED%9B%88&baseYmd=2021.08&accessToken=0789171e-8aa6-471f-a644-032a5b839d6d&id=' +
                    'PP150308&empKey=P9kqgAWyssF8%2B8fIhAr8mg==&orgNm=%EC%9D%B8%EC%82%AC%ED%8C%80&a' +
                    'uthCode=%5B%2220%22%2C%20%2230%22%2C%20%2235%22%2C%20%2250%22%2C%20%2255%22%2C' +
                    '%20%2260%22%2C%20%2270%22%2C%20%2275%22%2C%20%2299%22%5D'
                )
                .then(response => (this.OrganizationsData = response.data))
                .catch(function (error) { // 요청 실패 처리
                    console.log(error);
                });
            axios
                .get(
                    'https://8vxu0grpsd.execute-api.ap-northeast-2.amazonaws.com/ifm/api/ext/panpac' +
                    'ific/EIS_MONTH_CHILD?tenantKey=panpacific&locale=ko_US&userToken=3b4b963a-929d' +
                    '-4235-9ab6-2048a98c4859&empKey=P9kqgAWyssF8%2B8fIhAr8mg==&accessToken=0789171e' +
                    '-8aa6-471f-a644-032a5b839d6d&orgNm=%EC%9D%B8%EC%82%AC%ED%8C%80&baseYmd=2021.08' +
                    '&orgCd=10111&authCode=%5B%2220%22%2C%20%2230%22%2C%20%2235%22%2C%20%2250%22%2C' +
                    '%20%2255%22%2C%20%2260%22%2C%20%2270%22%2C%20%2275%22%2C%20%2299%22%5D&id=PP@1' +
                    '0005&empNm=%EC%B5%9C%EC%84%B8%ED%9B%88&compareYmd=2020.08'
                )
                .then(response => (this.PersonnalsData = response.data))
                .catch(function (error) { // 요청 실패 처리
                    console.log(error);
                });
            this.OrganizationsData = Organizations_of_local;
        },
        mounted() {
            this.inputHtml();
        },
        methods: {
            makingTable() {
                let stringHTML = '<colgroup><col width="30%;"><col width="20%;"><col width="20%;"><col width="*%' +
                        ';"></colgroup><tbody><tbody><tr><th colspan="4" class="step1">인원</th></tr><tr>' +
                        '<th rowspan="3" class="step2 line-bottom">태평양 물산</th><th colspan="2" class="st' +
                        'ep3">국내</th><td class="pay">0,000</td></tr><tr><th colspan="2" class="step3">주' +
                        '재원</th><td class="pay">0,000</td></tr><tr><td colspan="2" class="sub-total lin' +
                        'e-bottom line-top">합계</td><td class="sub-total pay line-bottom line-top">0,000' +
                        '</td></tr><tr><th rowspan="3" class="step2 line-bottom">소속 외</th><th colspan="' +
                        '2" class="step3">파견직/현채인</th><td class="pay">0,000</td></tr><tr><th colspan="2' +
                        '" class="step3">현지인</th><td class="pay">0,000</td></tr><tr><th colspan="2" cla' +
                        'ss="sub-total line-bottom line-top">합계</th><td class="sub-total pay line-botto' +
                        'm line-top">0,000</td></tr><tr><th colspan="3" class="total line-bottom">인원 총 ' +
                        '합계</th><td class="total pay line-bottom">0,000</td></tr><tr><th colspan="4" cl' +
                        'ass="step1">인건비(단위: 천원)</th></tr><tr><th rowspan="5" class="step2 line-bottom"' +
                        '>태평양 물산</th><th colspan="2" class="step3">국내급여</th><td class="pay">0,000</td><' +
                        '/tr><tr><th rowspan="3" class="step3">주재원</th><th class="step3">급여</th><td cla' +
                        'ss="pay">0,000</td></tr><tr><th class="step3">기타</th><td class="pay">0,000</td' +
                        '></tr><tr><th class="step3">합계</th><td class="pay">0,000</td></tr><tr><th cols' +
                        'pan="2" class="sub-total line-bottom line-top">합계</th><td class="pay sub-total' +
                        ' line-bottom line-top">0,000</td></tr><tr><th rowspan="3" class="step2 line-bo' +
                        'ttom">소속 외</th><th colspan="2" class="step3">파견직/현채인</th><td class="pay">0,000' +
                        '</td></tr><tr><th colspan="2" class="step3">현지인</th><td class="pay">0,000</td>' +
                        '</tr><tr><th colspan="2" class="sub-total line-bottom line-top">합계</th><td cla' +
                        'ss="sub-total pay line-bottom line-top">0,000</td></tr><tr><th colspan="3" cla' +
                        'ss="total line-bottom">인건비 총 합계</th><td class="total pay line-bottom">0,000</t' +
                        'd></tr><tr><th colspan="3" class="total-all line-bottom">인당 인건비(단위 : 천원)</th><' +
                        'td class="total-all pay line-bottom">0,000</td></tr></tbody></tbody>';
                return stringHTML;
            },
            inputHtml() {
                document
                    .getElementById('Organozations')
                    .appendChild(this.createHtml(this.OrganizationsData.result, 0));
                for (let Data of this.JsonKeyData) {
                    let setEventElement = document.getElementById(Data);
                    setEventElement.addEventListener('click', function (e) {
                        if (setEventElement.parentElement.className === 'menu') {
                            if (setEventElement.className === 'list') {
                                setEventElement.setAttribute('class', 'list active');
                            } else {
                                setEventElement.setAttribute('class', 'list');
                            }
                        } else {
                            if (setEventElement.className === 'list' && setEventElement.parentElement.parentElement.classList.contains('active')) {
                                setEventElement.setAttribute('class', 'list active');
                            } else {
                                setEventElement.setAttribute('class', 'list');
                            }
                        }
                        e.stopPropagation();
                        e.preventDefault();
                    });
                }
            },
            setBackGroundColor(level) {
                return 'rgb(' + (
                    50 + parseInt(level * 20)
                ) + ', ' + (
                    66 + parseInt(level * 30)
                ) + ', ' + (
                    82 + parseInt(level * 20)
                ) + ')';
            },
            createHtml(menuJson, level) {
                let mainUL = document.createElement('ul');
                if (this.firstcheck) {
                    mainUL.className = 'menu';
                } else {
                    mainUL.className = 'items';
                }
                for (let item of menuJson) {
                    if (item.dept) {
                        let li_Part = document.createElement('li');
                        li_Part.className = 'list';
                        li_Part.style.backgroundColor = this.setBackGroundColor(level);
                        li_Part.id = item.key;
                        this
                            .JsonKeyData
                            .push(item.key);
                        let a_Part = document.createElement('a');
                        a_Part.setAttribute('href', '#');
                        a_Part.addEventListener('click', function (e) {
                            e.preventDefault();
                        });
                        a_Part.textContent = item.title;
                        li_Part.appendChild(a_Part);
                        this.firstcheck = false;
                        li_Part.appendChild(this.createHtml(item.dept, level + 1));
                        mainUL.appendChild(li_Part);
                    } else {
                        let li_Part = document.createElement('li');
                        li_Part.className = 'Table-li';
                        li_Part.style.backgroundColor = this.setBackGroundColor(level);
                        let a_Part = document.createElement('a');
                        a_Part.textContent = item.title;
                        a_Part.setAttribute('href', '#');
                        let tempElement = document.createElement("table");
                        tempElement.className = "basic";
                        tempElement.style.display = "none";
                        tempElement.style.backgroundColor = this.setBackGroundColor(level+1);
                        tempElement.innerHTML = this.makingTable();
                        a_Part.addEventListener('click', function (e) {
                            if (tempElement.className === "basic") {
                                tempElement.className = "basic show";
                                tempElement.style.display = "";
                            } else {
                                tempElement.className = "basic";
                                tempElement.style.display = "none";
                            }
                            e.stopPropagation();
                            e.preventDefault();
                        });
                        li_Part.appendChild(a_Part);
                        li_Part.appendChild(tempElement);
                        mainUL.appendChild(li_Part);
                    }
                }
                return mainUL;
            }
        }
    }
</script>
<style>
    .basic {
        width: 95%;
        border: black;
        margin: 3%;
    }
    td,
    th {
        border: 1px solid black;
    }
    ul.tab-wrap {
        padding: 0;
        list-style: none;
        width: 700px;
        margin: 20px auto;
        font-family: 'Roboto';
        box-shadow: 0 0 25px #00000070;
        clear: both;
        display: table;
    }
    ul.tab-wrap > li {
        font-size: 14px;
        border-bottom: 1px solid #324252;
        position: relative;
        width: 100%;
        box-sizing: border-box;
        height: 50px;
        vertical-align: sub;
        background: #3e5165;
        clear: both;
    }
    ul.tab-wrap > li > a {
        text-decoration: none;
        color: #fff;
        padding: 17px 0 17px 45px;
        display: block;
        height: 100%;
        box-sizing: border-box;
    }
    ul.menu {
        padding: 0;
        list-style: none;
        width: 700px;
        margin: 20px auto;
        font-family: 'Roboto';
        box-shadow: 0 0 25px #00000070;
        clear: both;
        display: table;
    }
    ul.menu .list {
        font-size: 14px;
        border-bottom: 1px solid #324252;
        position: relative;
        width: 100%;
        box-sizing: border-box;
        height: 50px;
        vertical-align: sub;
        background: #3e5165;
        clear: both;
    }
    ul.menu .list:after {
        content: '·';
        font-family: FontAwesome;
        position: absolute;
        right: 17px;
        top: 17px;
        padding: 0 5px;
        color: #fff;
    }
    ul.menu .list:before {
        content: '·';
        font-family: FontAwesome;
        position: absolute;
        left: 17px;
        top: 17px;
        padding: 0 5px;
        color: #fff;
    }
    ul.menu .list a {
        text-decoration: none;
        color: #fff;
        padding: 17px 0 17px 45px;
        display: block;
        height: 100%;
        box-sizing: border-box;
    }
    ul.menu .list a:hover {
        background-color: #324252;
        transition: 300ms all;
        color: #09fbd2;
    }
    ul.menu .list .items {
        height: 0;
        overflow: hidden;
    }
    ul.menu .list .items a {
        padding: 17px;
    }
    ul.menu .list .items a:hover {
        background-color: #3f5d79;
        color: #fff;
        transition: 300ms all;
    }
    ul.menu .list:last-child {
        border-bottom: none;
    }
    ul.menu .active:after {
        font-family: FontAwesome;
        position: absolute;
        right: 17px;
        top: 17px;
        padding: 0 5px;
        color: #fff;
    }
    ul.menu .active:before {
        font-family: FontAwesome;
        position: absolute;
        left: 17px;
        top: 17px;
        padding: 0 5px;
        color: #fff;
    }
    ul.menu .active > .items {
        display: block;
        background: #23313f;
        padding: 0;
        height: auto;
        color: #fff;
        transition-timing-function: cubic-bezier(0.075, 0.82, 0.165, 1);
        transition: all 200ms;
        clear: both;
        float: left;
        width: 100%;
    }
    ul.menu .active > .items li {
        padding: 0;
        border-bottom: 1px solid #324252;
        list-style: none;
    }
    ul.menu .active > .items li:last-child {
        border-color: transparent;
        padding-bottom: 0;
    }
    ul.menu .active > .items .active > .items {
        background-color: #2f4b67;
    }
    ul.menu .active > a {
        color: #46efa4;
        text-transform: uppercase;
        font-weight: bold;
    }
    ul.menu .active .list {
        background: #697d92;
    }
    ul.menu .active .list a {
        padding: 17px 0 17px 45px;
    }
</style>