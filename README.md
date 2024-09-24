# replit_projects
projects exported from replit



After their free changes were implemented and they limited the capability to save projects and code to 3 files ( <50 Mb each, or $100/year ), I decided to move my code here for safekeeping.

100 days of Python code - from introductory to more advanced topics
Day 1: 
Day 2: 
Day 3: 
Day 4: 
Day 5: 
Day 6: 
Day 7: 
Day 8: 
Day 9: 
Day 10: 
Day 11: 
Day 12: 
Day 13: 
Day 14: 
Day 15: 
Day 16: 
Day 17: 
Day 18: 
Day 19: 
Day 20: 
Day 21: 
Day 22: 
Day 23: 
Day 24: 
Day 25: 
Day 26: 
Day 27: 
Day 28: 
Day 29: 
Day 30: 
Day 31: 
Day 32: 
Day 33: 
Day 34: 
Day 35: 
Day 36: 
Day 37: 
Day 38: 
Day 39: 
Day 40: 
Day 41: 
Day 42: 
Day 43: 
Day 44: 
Day 45: 
Day 46: 
Day 47: 
Day 48: 
Day 49: 
Day 50: 
Day 51: 
Day 52: 
Day 53: 
Day 54: 
Day 55: 
Day 56: 
Day 57: 
Day 58: 
Day 59: 
Day 60: 
Day 61: 
Day 62: 
Day 63: 
Day 64: 
Day 65: 
Day 66: 
Day 67: 
Day 68: 
Day 69: 
Day 70: 
Day 71: 
Day 72: 
Day 73: 
Day 74: 
Day 75: 
Day 76: 
Day 77: 
Day 78: 
Day 79: 
Day 80: 
Day 81: 
Day 82: 
Day 83: 
Day 84: 
Day 85: 
Day 86: 
Day 87: 
Day 88: 
Day 89: 
Day 90: 
Day 91: 
Day 92: 
Day 93: 
Day 94: 
Day 95: 
Day 96: 
Day 97: 
Day 98: 
Day 99: 
Day 100: 







Script from funnyfishwalter at reddit <https://www.reddit.com/r/replit/comments/1f2xv9p/guide_how_to_export_your_data_and_leave_replit/> and https://github.com/hackermondev/replit-exporter


function isAtBottom() {
    return (window.innerHeight + window.scrollY) >= document.documentElement.scrollHeight;
}

function promptUser(items) {
    let format = '';
    items.forEach(item => format += `<a href='${item}'>${item}</a><br>`);

    document.write(`<html style='font-family: sans-serif'><head><title>Your Repl Files</title></head><body><h1>Success!</h1><br><h3>Your Replit files have been successfully fetched.</h3><button onclick="downloadAll();">Download All</button><br><br><br>${format}</body></html>`);

    const script = document.createElement('script');
    script.textContent = `
        function downloadAll() {
            const items = ${JSON.stringify(items)};
            
            items.forEach(item => window.open(item));
        }
    `;
    document.body.appendChild(script);
}

function finishSetup() {
    let items = [];
    console.log('Process complete! Fetching all Repls...');
    
    document.querySelectorAll('.css-ow5df0 a').forEach(element => {
        let currentHref = new URL(element.href);
        currentHref.search = '';
        let newHref = currentHref.toString() + '.zip';

        items.push(newHref);
    });

    promptUser(items);
}

function scrollToBottom() {
    const scrollSpeed = 300;
    
    function performScroll() {
        window.scrollBy(0, scrollSpeed);
        
        if (isAtBottom()) {
            console.log('Checking if any more Repls are available...');
            
            setTimeout(function() {
                if(isAtBottom() && !document.querySelector('.load-more-spinner')) {
                    // this will run if they're still at the bottom after 2 seconds and the page is not loading (meaning it's complete, i know i know, it's not the most reliable thing ever but I don't have a choice)
                    finishSetup();
                } else {
                    requestAnimationFrame(performScroll);
                }
            }, 2000);
        } else {
            requestAnimationFrame(performScroll);
        }
    }
    
    requestAnimationFrame(performScroll);
}

console.clear();
scrollToBottom();
