/**
 * Polyfill to allow CSS automatic grid placement in IE11 
 * Requires a data-grid-cols="n" to be specified on the grid container
 * Requires col span classes to include the number of colums as such colspan2, colspan3, etc
 */
function placeItems(grid) {
    let curColSpans = 0,
        curRow = 1,
        curCol = 1,
        totalCols = grid.getAttribute('data-grid-cols');
    toArray(grid.children).forEach(function(item) {
        let colSpan = 1;
        for (let i = 0; i <= totalCols; i++) {
            if (item.classList.contains('colspan'+i)) {
                colSpan = i;
                break;
            }
        }
        let exceedsColCount = curColSpans + Number(colSpan) > totalCols;
        if (exceedsColCount) {
            curRow += 1;
            curColSpans = 0;
            curCol = 1;
        }
        curColSpans = curColSpans + Number(colSpan);
        itemStyles = '-ms-grid-row: ' + curRow + '; -ms-grid-column: ' + curCol + '; -ms-grid-column-span: ' + colSpan + '; margin-right: 5px; margin-left: 5px;';
        item.setAttribute('style', itemStyles);
        curCol += colSpan;
    });
}
function cssGridPolyfill() {
    const grids = document.querySelectorAll('[data-grid-cols]');
    toArray(grids).forEach(function(item){ placeItems(item) });
}
function toArray(o) {
    return Array.prototype.slice.call(o);
}
const supportsGrid = typeof CSS !== 'undefined'
        && typeof CSS.supports !== 'undefined'
        && CSS.supports('display', 'grid');
if (!supportsGrid) {
    document.addEventListener('DOMContentLoaded', cssGridPolyfill);
    
    var mutationObserver = new MutationObserver(function(mutations) {
        mutations.forEach(function(mutation) {
            cssGridPolyfill();
        });
    });
    
    mutationObserver.observe(document.documentElement, {
        childList: true,
        subtree: true,
    });
}