
Array
  .from(document.querySelectorAll("h1, h2, h3, h4"))
  .map(el => {
    let spaces = " ".repeat((parseInt(el.tagName[1])-1)*2)}
    let text = el.outerText.replace(/\:$/, '')
    return `${spaces}- ${text}`
   })
  .join("\n")