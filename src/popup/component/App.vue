<template>
    <div v-if="aut == 'AUTH_LOAD'">
        <div class="text-center"><svg width='120px' height='120px' xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" preserveAspectRatio="xMidYMid" class="uil-default"><rect x="0" y="0" width="100" height="100" fill="none" class="bk"></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(0 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(30 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.08333333333333333s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(60 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.16666666666666666s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(90 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.25s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(120 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.3333333333333333s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(150 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.4166666666666667s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(180 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.5s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(210 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.5833333333333334s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(240 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.6666666666666666s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(270 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.75s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(300 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.8333333333333334s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(330 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.9166666666666666s' repeatCount='indefinite'/></rect></svg></div>
    </div>
    <div v-else-if="aut == 'AUTH_SUCCESS'">
        <nav class="navbar navbar-default" role="navigation" style="padding: 0 10px;">
            <div class="container-fluid">
                <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                    <ul class="nav navbar-nav">
                        <li :class="{active: (navBarActive == 'all')}">
                            <a href="#" v-on:click="changeNavBarActive('all')">Все ({{ navBarCount.positive + navBarCount.negative }})</a>
                        </li>
                        <li :class="{positive: true, active: (navBarActive == 'positive')}">
                            <a href="#" v-on:click="changeNavBarActive('positive')">Положительные ({{ navBarCount.positive }})</a>
                        </li>
                        <li :class="{negative: true, active: (navBarActive == 'negative')}">
                            <a href="#" v-on:click="changeNavBarActive('negative')">Отрицательные ({{ navBarCount.negative }})</a>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
        <div style="float: right; margin: -10px 0px 10px 10px;">
            <a class="review-button-add" :href="BASE_DOMAIN + 'reviews/add?url=' + currentTabUrl" target="_blank">Добавить отзыв о сайте</a>
        </div>
        <div style="clear: both;"></div>
        <div class="site-reviews-list" v-html="siteReviewsList"></div>
        <ul class="navigation-pages" v-if="paginator.all > 1">
            <li v-for="i in paginator.all" :class="{active: (i == paginator.current)}">
                <span v-if="(i == paginator.current)">{{ i }}</span>
                <a href="#" v-on:click="filterPage(i)" v-if="(i != paginator.current)"><span>{{ i }}</span></a>
            </li>
        </ul>
        <div class="paginator text-center sublink">
            <a href="http://web-ratings.ru/reviews_top" class="review-button-add" target="_blank">ТОП сайтов</a>
            <a href="http://web-ratings.ru/user_sites" class="review-button-add" target="_blank">Мои сайты</a>
            <a href="http://web-ratings.ru/user_profile" class="review-button-add" target="_blank">Настройки</a>
            <a href="http://web-ratings.ru/user_verification" class="review-button-add" target="_blank">Верификация</a>
        </div>
    </div>
    <div v-else-if="aut == 'AUTH_FAIL'">
        <div class="text-center">
            <div class="col-xs-12" style="margin-top: 52px;">
                <a class="review-button-add" :href="BASE_DOMAIN + 'reviews/add?url=' + currentTabUrl" target="_blank">Отзывов о сайте нет, оставьте отзыв первым</a>
            </div>
        </div>
    </div>
    <div v-else>
        Не понятно
    </div>
</template>

<script type="text/babel">
    import 'bootstrap';
    import './../../asset/css/my.css';
    import './../../asset/css/style.css';

    import {BASE_DOMAIN, AUTH_LOAD, AUTH_SUCCESS, AUTH_FAIL} from './../constant.js';

    console.info('BASE_DOMAIN = ', BASE_DOMAIN);

    export default {
        data() {
            setTimeout(() => {
                this.checkAuth();
            }, 1000);
            return {
                BASE_DOMAIN: BASE_DOMAIN,
                aut: AUTH_LOAD,
                currentTabUrl: '',

                navBarActive: 'all',
                navBarCount: {
                    positive: 0,
                    negative: 0,
                },
                paginator: {
                    all: 0,
                    current: 0
                },
                siteReviewsList: '',
            };
        },
        methods: {
            checkAuth: function () {
                chrome.tabs.query({active: true, currentWindow: true}, (tabs) => {
                    var currentTabUrl = tabs[0].url;
                    //currentTabUrl = 'http://web-ratings.ru/';// TODO: Удалить
                    this.currentTabUrl = this.getLocation(currentTabUrl).hostname.replace(/^www\./, '');
                    console.log('currentTabUrl = ', this.currentTabUrl);
                    this.loadSiteReviewsList();
                });
            },
            changeNavBarActive (rate) {
                this.navBarActive = rate;
                this.paginator.current = 1;
                this.loadSiteReviewsList();
            },
            filterPage (page) {
                this.paginator.current = page;
                this.loadSiteReviewsList();
            },
            loadSiteReviewsList(){
                var url = BASE_DOMAIN + 'site/' + this.currentTabUrl + '?';

                if (this.navBarActive != 'all') {
                    url += '&rate=' + this.navBarActive;
                }
                if (this.paginator.current > 1) {
                    url += '&page=' + this.paginator.current;
                }
                console.info('url = ', url);

                $.ajax({
                    url: url,
                    dataType: 'html',
                    type: 'get'
                }).done((data) => {
                    console.info('checkAuth.done | data = ', data);
                    var s = data.indexOf('Репутация сайта');
                    console.info('checkAuth.done | s = ', s);
                    if (s == -1) {
                        this.aut = AUTH_FAIL;
                    } else {
                        this.aut = AUTH_SUCCESS;
                        this.drawSiteReviewsList(data);
                    }
                }).fail((jqXHR, textStatus, errorThrown) => {
                    console.info('checkAuth.fail | jqXHR = ', jqXHR);
                    console.info('checkAuth.fail | textStatus = ', textStatus);
                    this.aut = AUTH_FAIL;
                });
            },
            drawSiteReviewsList(data){
                data = $(data);
                var siteReviewsList = data.find('.site-reviews-list');
                siteReviewsList.find('.voting').remove();
                siteReviewsList.find('a').each(function () {
                    var t = $(this).text();
                    $(this).replaceWith(t);
                });
                siteReviewsList.find('[onclick]').attr('onclick', '');
                siteReviewsList.find('[title]').attr('title', '');
                siteReviewsList.find('.navigation-pages').remove();
                siteReviewsList = siteReviewsList.html();
                siteReviewsList = siteReviewsList.replace(/background\-image: url\('/g, 'background-image: url(\'http:')
                this.siteReviewsList = siteReviewsList;

                var navBarCount = {};
                $.each(['positive', 'negative'], function (i, type) {
                    var val = data.find('li.' + type).text().match(/\((\d+)\)/);
                    console.info('val = ', val);
                    navBarCount[type] = parseInt(val[1]);
                });
                console.info('navBarCount = ', navBarCount);
                this.navBarCount = navBarCount;

                var paginator = {
                    all: 1,
                    current: 1
                };
                if (data.find('.navigation-pages').length) {
                    paginator.current = parseInt(data.find('.navigation-pages li.active span').text());
                    paginator.all = Math.max(
                        parseInt(data.find('.navigation-pages li a').last().attr('href').match(/page=(\d+)/)[1]),
                        parseInt(data.find('.navigation-pages li.active span').text())
                    );
                }
                console.info('paginator = ', paginator);
                this.paginator = paginator;
            },
            getLocation (href) {
                var l = document.createElement("a");
                l.href = href;
                return l;
            }
        },
        components: {}
    }
</script>