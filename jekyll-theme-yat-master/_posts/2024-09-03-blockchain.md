---
layout: post
title: 블록체인 이론 및 응용
subtitle: k-mooc / Prof. Won-Ki Hong, POSTECH
excerpt_image: /assets/images/blockchain.png
categories: study
tags: [Blockchain, Cryptography] 
top: 2
---

![banner](/assets/images/blockchain.png)

### 왜 블록체인인가 ###

|구글은 어떻게 여성을 차별하는가<br>(사피야 우모자)  | 설명          |
|:-----------------------:|:---------------------:|
| ![Book](/assets/images/book_algorithms_of_oppression.jpg)   |  <div style="text-align: justify;">  이 책은 it 기업이 데이터를 수집하고 처리하는 방식에서 여성을 비롯해 흑인과 유대인 등의 특정 집단이 차별받고 있음을 고발한다.<br> 블록체인의 투명성을 이용한다면 의도적 혐오 조장, 나아가 알고리즘 편향을 차단할 수 있지 않을까 생각했다.<br>  k-mooc에서 블록체인 이론에 관한 강의를 수강하였고, 추후 블록체인을 이용한 스마트컨트랙트를 구현해보며 블록체인을 응용해보고자 한다.</div> |

<br>

### k-mooc 강의 정리
* <h4 style="color: navy;">W1. Intro: 블록체인 핵심 기술과 활용 범위</h4>


<div>
    <button id="prev-page1">이전 페이지</button>
    <input type="text" id="page-input1" placeholder="페이지 번호 입력" />
    <button id="go-to-page1">이동</button>
    <button id="next-page1">다음 페이지</button>
    <span id="page-info1"></span> <!-- 페이지 정보 표시 -->
</div>
<div id="pdf-viewer1" style="width: 100%; height: 600px; margin-bottom: 300px;"></div>



* <h4 style="color: navy;"> W2. Mechanics of Bitcoin: 암호학, 블록, 트랜잭션</h4>



<div>
    <button id="prev-page2">이전 페이지</button>
    <input type="text" id="page-input2" placeholder="페이지 번호 입력" />
    <button id="go-to-page2">이동</button>
    <button id="next-page2">다음 페이지</button>
    <span id="page-info2"></span> <!-- 페이지 정보 표시 -->
</div>
<div id="pdf-viewer2" style="width: 100%; height: 600px; margin-bottom: 300px;"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.10.377/pdf.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.10.377/pdf.worker.min.js"></script>

<script>
    // PDF 파일 경로 설정
    const pdfUrls = [
        '{{ site.baseurl }}/assets/files/week1.pdf', // 첫 번째 PDF 파일 경로
        '{{ site.baseurl }}/assets/files/week2.pdf'  // 두 번째 PDF 파일 경로
    ];

    let pdfDocs = [null, null],
        pageNums = [1, 1],
        pageIsRendering = [false, false],
        pageNumIsPending = [null, null];

    // PDF.js 설정
    pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.10.377/pdf.worker.min.js';

    // PDF 문서 로드
    pdfUrls.forEach((url, index) => {
        pdfjsLib.getDocument(url).promise.then(pdfDoc_ => {
            pdfDocs[index] = pdfDoc_;
            renderPage(index, pageNums[index]);
        });
    });

    // 페이지 렌더링 함수
    const renderPage = (index, num) => {
        pageIsRendering[index] = true;

        pdfDocs[index].getPage(num).then(page => {
            const viewport = page.getViewport({ scale: 1 });
            const canvas = document.createElement('canvas');
            const ctx = canvas.getContext('2d');
            canvas.height = viewport.height;
            canvas.width = viewport.width;

            document.getElementById(`pdf-viewer${index + 1}`).innerHTML = ''; // 이전 페이지 삭제
            document.getElementById(`pdf-viewer${index + 1}`).appendChild(canvas);

            const renderCtx = {
                canvasContext: ctx,
                viewport: viewport
            };

            page.render(renderCtx).promise.then(() => {
                pageIsRendering[index] = false;

                if (pageNumIsPending[index] !== null) {
                    renderPage(index, pageNumIsPending[index]);
                    pageNumIsPending[index] = null;
                }

                // 페이지 정보 업데이트
                document.getElementById(`page-info${index + 1}`).textContent = `페이지 ${pageNums[index]} / ${pdfDocs[index].numPages}`;
            });
        });

        document.getElementById(`page-input${index + 1}`).value = num; // 페이지 번호 업데이트
    };

    // 페이지 이동 버튼 이벤트
    const setupPageNavigation = (index) => {
        document.getElementById(`go-to-page${index + 1}`).addEventListener('click', () => {
            const pageInput = document.getElementById(`page-input${index + 1}`).value;
            const num = parseInt(pageInput);

            if (num > 0 && num <= pdfDocs[index].numPages) {
                pageNums[index] = num;
                renderPage(index, pageNums[index]);
            }
        });

        document.getElementById(`prev-page${index + 1}`).addEventListener('click', () => {
            if (pageNums[index] <= 1) return; // 첫 페이지에서 이전 페이지 이동 방지
            pageNums[index]--;
            renderPage(index, pageNums[index]);
        });

        document.getElementById(`next-page${index + 1}`).addEventListener('click', () => {
            if (pageNums[index] >= pdfDocs[index].numPages) return; // 마지막 페이지에서 다음 페이지 이동 방지
            pageNums[index]++;
            renderPage(index, pageNums[index]);
        });
    };

    // 각 PDF에 대해 페이지 탐색 기능 설정
    pdfUrls.forEach((_, index) => setupPageNavigation(index));
</script>

### 추후 공부 계획
<iframe src="https://www.inflearn.com/course/%EB%B8%94%EB%A1%9D%EC%B2%B4%EC%9D%B8-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%BD%94%EC%9D%B8%EC%A0%9C%EC%9E%91/dashboard" style="width:100%; height:500px;" frameborder="0"></iframe>

<br><br>현재 인프런에서 위 강의를 수강하고 있다. 실습을 통해 블록체인의 기본 언어인 솔리디티를 익히고, 방학 때 스마트 컨트랙트를 이용한 프로젝트를 진행하고자 한다.