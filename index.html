// ==UserScript==
// @name         Yiban
// @namespace    http://tampermonkey.net/
// @version      0.2
// @description  Bypass!
// @author       MaDragon
// @icon         https://www.google.com/s2/favicons?sz=64&domain=microsoft.com
// @grant        none
// @match        *://exam.yooc.me/group/*/exam/*
// @require      https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.9/crypto-js.min.js
// ==/UserScript==

(async function () {

    'use strict';


    var message = "MaDragon提示您，本脚本仅限技术交流，请勿用于其他用途，否则一切后果由您本人承担！！！";


    const styleTag = document.createElement('style');
    styleTag.innerHTML = `
    .watermark-container {
        position: fixed;
        width: 200px;
        height: 100px;
        pointer-events: none;
        z-index: 9999;
    }

    .watermark-text {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%) rotate(-45deg);
        opacity: 0.5;
        font-size: 24px;
        color: #000;
    }
`;

    const watermarks = [
        { text: 'MaDragon', top: '20px', left: '20px' },
        { text: 'MaDragon', top: '50%', left: '50%' },
        { text: 'MaDragon', top: 'calc(100% - 120px)', left: 'calc(100% - 220px)' }
    ];

    const watermarkFragment = document.createDocumentFragment();

    watermarks.forEach((watermark) => {
        const watermarkContainer = document.createElement('div');
        watermarkContainer.classList.add('watermark-container');
        watermarkContainer.style.top = watermark.top;
        watermarkContainer.style.left = watermark.left;

        const watermarkText = document.createElement('div');
        watermarkText.classList.add('watermark-text');
        watermarkText.innerText = watermark.text;

        watermarkContainer.appendChild(watermarkText);
        watermarkFragment.appendChild(watermarkContainer);
    });

    document.body.appendChild(watermarkFragment);
    document.head.appendChild(styleTag);

    async function request(url, options) {
        const response = await fetch(url, options);
        const resJson = await response.json();
        return resJson;
    }

    function unescapeHTML(str) {
        const map = {
            '&lt;': '<',
            '&gt;': '>',
            '&quot;': '"',
            '&#39;': "'",
            '&amp;': '&',
            '&nbsp;': ' ',
            '&copy;': '©',
            '&reg;': '®',
            '&trade;': '™',
            '&euro;': '€',
            '&pound;': '£',
            '&yen;': '¥',
            '&cent;': '¢'
        };

        return str.replace(/&(lt|gt|quot|#39|amp|nbsp|copy|reg|trade|euro|pound|yen|cent);/g, (m, entity) => map[m]);
    }
    const examIdMatch = window.location.href.match(/exam\/([0-9]+)?/);
    const examId = examIdMatch ? examIdMatch[1] : null;

    let userId, token, yibanId;
    const userIdMatch = document.cookie.match(/user_id=([0-9]+)?/);
    const tokenCookie = document.cookie.split(';').find(cookie => cookie.includes('user_token'));
    const yibanIdCookie = document.cookie.split(';').find(cookie => cookie.includes('yiban_id'));

    if (userIdMatch && tokenCookie && yibanIdCookie) {
        userId = userIdMatch[1];
        token = tokenCookie.split('=')[1];
        yibanId = yibanIdCookie.split('=')[1];
    } else {
        location.replace(location.href);
    }

    const nx = (e, r = false) => {
        const a = "yooc@admin";
        const c = CryptoJS.enc.Utf8.parse(CryptoJS.MD5(a + yibanId).toString().substring(8, 24));
        const l = CryptoJS.enc.Utf8.parse("42e07d2f7199c35d");

        if (r) e = a + e;

        return CryptoJS.AES[r ? "encrypt" : "decrypt"](
            e, c, {
            iv: l,
            mode: CryptoJS.mode.CBC
        }).toString(r ? "" : CryptoJS.enc.Utf8);
    };

    await new Promise(resolve => setTimeout(resolve, 100));
    alert(message);

    const examuserId = (await request(`https://exambackend.yooc.me/api/exam/setting/get?examId=${examId}&userId=${userId}&token=${token}&yibanId=${yibanId}`)).data.examuserId;

    const datas = (await request(`https://exambackend.yooc.me/api/exam/paper/get?examuserId=${examuserId}&token=${token}&yibanId=${yibanId}`));

    const decrypted = (encrypted, type, choices = []) => JSON.parse(nx(encrypted, false)).map(x => type === "completion" ? (x.join ? x.join(' | ') : x) : String.fromCharCode(65 + (choices && choices.length ? choices.indexOf(~~x) : ~~x))).join("、");

    const subjects = datas.data.flatMap(sec => sec.subjects);
    const answers = subjects.map(subj => decrypted(subj.answer, subj.type));

    subjects.forEach((subj, i) => {
        subj.decode_answer = answers[i];

        subj.right_options = [];
        subj.right = [];

        for (let j = 0; j < subj.decode_answer.length; j++) {
            const t = subj.decode_answer[j];
            if (t !== "、") {
                const optionIndex = t.charCodeAt(0) - "A".charCodeAt(0);
                const optionContent = subj.option[optionIndex];
                const option = {
                    options: t,
                    content: optionContent
                };
                subj.right_options.push(optionContent);
                subj.right.push(option);
            }
        }
    });

    function clickWithDelay(element) {
        setTimeout(function () {

            element.dispatchEvent(new MouseEvent('click', {
                bubbles: true,
                cancelable: true,
                view: window
            }));
        }, 200);
    }
    function click(element) {
        setTimeout(function () {

            element.dispatchEvent(new MouseEvent('click', {
                bubbles: true,
                cancelable: true,
                view: window
            }));
        }, 800);
    }

    const createToggleButton = () => {
        const toggleBtn = document.createElement("button");
        toggleBtn.id = "toggle-btn";
        toggleBtn.textContent = "自动答题";
        toggleBtn.className = "hover-button";
        toggleBtn.style.position = "fixed";
        toggleBtn.style.boxShadow = "0 8px 17px 0 rgba(237,202,202,0.2), 0 6px 20px 0 rgba(0,0,0,.19)";
        toggleBtn.style.zIndex = "50";
        toggleBtn.style.width = "80px"; // 调整大小
        toggleBtn.style.height = "80px"; // 调整大小
        toggleBtn.style.borderRadius = "50%"; // 变成圆形
        toggleBtn.style.border = "none";
        toggleBtn.style.right = "38rem"; // 调整位置
        toggleBtn.style.top = "2rem"; // 调整位置
        toggleBtn.style.background = "linear-gradient(135deg, #00aaff, #0077cc)"; // 应用渐变背景
        toggleBtn.style.color = "#ffffff";
        toggleBtn.style.fontSize = "16px";
        toggleBtn.style.lineHeight = "80px"; // 垂直居中文本
        toggleBtn.style.textAlign = "center";
        toggleBtn.style.cursor = "pointer";


        // 拖拽按钮逻辑
        var isDragging = false;
        var dragOffset = { x: 0, y: 0 };

        toggleBtn.addEventListener('mousedown', function (e) {
            isDragging = true;
            dragOffset.x = e.clientX - toggleBtn.offsetLeft;
            dragOffset.y = e.clientY - toggleBtn.offsetTop;
        });

        document.addEventListener('mousemove', function (e) {
            if (isDragging) {
                toggleBtn.style.left = e.clientX - dragOffset.x + 'px';
                toggleBtn.style.top = e.clientY - dragOffset.y + 'px';
            }
        });

        document.addEventListener('mouseup', function (e) {
            isDragging = false;
        });

        toggleBtn.addEventListener('touchstart', function(e) {
            isDragging = true;
            dragOffset.x = e.touches[0].clientX - toggleBtn.offsetLeft;
            dragOffset.y = e.touches[0].clientY - toggleBtn.offsetTop;
        });

        document.addEventListener('touchmove', function(e) {
            if (isDragging) {
                toggleBtn.style.left = e.touches[0].clientX - dragOffset.x + 'px';
                toggleBtn.style.top = e.touches[0].clientY - dragOffset.y + 'px';
            }
        });

        document.addEventListener('touchend', function(e) {
            isDragging = false;
        });
        return toggleBtn;
    };




    const parentElement = document.body;
    const toggleBtn = createToggleButton();
    parentElement.insertBefore(toggleBtn, parentElement.firstChild);

    const buttons = document.getElementsByClassName("jsx-751469096");
    clickWithDelay(buttons.item(2));
    clickWithDelay(buttons.item(1));

    let autoClickEnabled = false;

    toggleBtn.addEventListener("click", () => {
        autoClickEnabled = !autoClickEnabled;
        toggleBtn.textContent = autoClickEnabled ? "自动答题" : "关闭";
        clickWithDelay(buttons.item(2));
    });

    function executeOnElementAvailable() {
        const ansTag = document.createElement("li");
        ansTag.setAttribute("id", "answer");
        ansTag.classList.add("jsx-2160564469", "flex", "items-center");
        ansTag.style.color = "red";

        const observer = new MutationObserver((mutations) => {
            mutations.forEach((mutation) => {
                const newValue = mutation.target.data;
                const divElements = document.querySelectorAll('div.jsx-2550022912.flex-auto, div.jsx-2160564469.flex-auto');

                ansTag.innerHTML = `第${newValue}题选项：${subjects[newValue - 1].decode_answer}（${subjects[newValue - 1].answer}）`;
                ansTag.innerHTML += "<br>"; // 添加换行
                ansTag.innerHTML += `第${newValue}题答案（以此为准）：${subjects[newValue - 1].right_options.join("    |    ")}`;
                divElements.forEach((div) => {
                    div.style.color = "";
                    div.style.fontFamily = "";
                    div.style.fontWeight = "";
                    div.style.fontSize = "";
                });

                subjects[newValue - 1].right.forEach((option) => {
                    let options_content = option.content.toString();
                    const convertedString = unescapeHTML(options_content);
                    let mark = option.options;
                    divElements.forEach((div) => {
                        const searchText = div.textContent.substring(2);
                        const text_mark = div.textContent[0];
                        if (searchText == options_content || searchText == convertedString) {
                            div.style.color = "orange";
                            div.style.fontFamily = "Arial, sans-serif";
                            div.style.fontWeight = "bold";
                            div.style.fontSize = "16px";
                            var parentDiv = div.parentNode;
                            if (autoClickEnabled) {
                                clickWithDelay(parentDiv);
                            }
                        }
                    });
                });
                if (autoClickEnabled) {
                    click(buttons.item(2));
                }
            });
        });

        const observeQuestionNumTag = () => {
            const questionNumTag = document.getElementsByClassName("jsx-3527395752").item(3);
            if (questionNumTag) {
                observer.observe(questionNumTag, { characterData: true, subtree: true });
            } else {
                setTimeout(observeQuestionNumTag, 100);
            }
        };

        const observeRootElement = () => {
            const rootElement = document.getElementsByClassName("jsx-3643416060").item(0);
            if (rootElement) {
                rootElement.parentElement.appendChild(ansTag);
                observeQuestionNumTag();
            } else {
                setTimeout(observeRootElement, 100);
            }
        };

        observeRootElement();
    }

    if (document.readyState === "complete" || document.readyState === "interactive") {
        executeOnElementAvailable();
    } else {
        document.addEventListener("DOMContentLoaded", executeOnElementAvailable);
    }
})();
