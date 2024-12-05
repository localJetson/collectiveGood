//Extract the elements on a html and places them in a given array, that have a matching attribute in the open tag. ej <div class="imported">
function extract_element_tag_attribute(given_html, given_tagName, given_attribute, temp_list){
  //Clears the arrays previous content
  text_list.length = 0

  var indx_ref = 0;
  var indx_attr;

  //Creates the tags of interest
  var tagOpening = "<" + given_tagName;
  var tagClosing = "</" + given_tagName + ">";

  //Loops until it reaches and exit condition.
  while(true){
    //Searches for the first instance of the open tag, if not there it breaks.
    var indx_tag_str = given_html.indexOf(tagOpening, indx_ref);
    if(indx_tag_str === -1) { break; }

    //Searches for the end of the tag of interest.
    var indx_tag_end = given_html.indexOf('>', indx_tag_str);
    if(indx_tag_end === -1) { break; }

    //Records the indx of the last point of interest for next loop to start from
    indx_ref = indx_tag_end+1;

    //Searches for the attribute in the html
    indx_attr = given_html.indexOf(given_attribute, indx_tag_str);

    //If the attribute is found and it exist before the closing tag then it's 'accepted', else it loops from the last point of interest to look for the next tag.
    if(indx_attr !== -1 && indx_attr < indx_tag_end){
      var probe_open  = indx_tag_end + 1;
      var probe_close = indx_tag_end + 1;

      //Here we are going to look for the appropiate closing tag that belongs to our parent. This is to distinguish closing tags that belong to childrens with the same opening tag. Ej <div> <div> <\div> <\div>
      while(true){
        probe_open  = given_html.indexOf(tagOpening, probe_open ); //Looks for the next opening tag
        probe_close = given_html.indexOf(tagClosing, probe_close); //Looks for the next closing tag

        if(probe_close === -1)        { return -1; } //This should never really happen but just in case to keep the logic sound.
        if(probe_open  === -1)        { break;     } //This condition means there's no more children with the same tag as the parent therefore the closing tag found belong to them.
        if(probe_open > probe_close)  { break;     } //This condition means that the opening tag exist outside of the parent tag and therefore the closing tag foung belong to them.

        probe_open++;
        probe_close++;
      }

      text_list.push(given_html.substring(indx_tag_str, probe_close + tagClosing.length));
    }
  }

  return text_list.length;
}

//Copy paste of the previous one without the check for attributes. might be best to just run this one and if you're looking for a specific attribute run through the list and extract the ones of interest.
function extract_element_tag(given_html, given_tagName, text_list){
  text_list.length = 0

  var indx_ref = 0;
  var tagOpening = "<" + given_tagName;
  var tagClosing = "</" + given_tagName + ">";

  while(true){
    var indx_tag_str = given_html.indexOf(tagOpening, indx_ref);
    if(indx_tag_str === -1) { break; }

    var indx_tag_end = given_html.indexOf('>', indx_tag_str);
    if(indx_tag_end === -1) { break; }
    
    indx_ref = indx_tag_end+1;

    var probe_open  = indx_tag_end + 1;
    var probe_close = indx_tag_end + 1;

    while(true){
      probe_open  = given_html.indexOf(tagOpening, probe_open );
      probe_close = given_html.indexOf(tagClosing, probe_close);

      if(probe_close === -1)        { return -1; }
      if(probe_open  === -1)        { break;     }
      if(probe_open > probe_close)  { break;     }

      probe_open++;
      probe_close++;
    }

    text_list.push(given_html.substring(indx_tag_str, probe_close + tagClosing.length));
  }

  return text_list.length;
}

//Some sample use case
function temp(){
  var source_html = get_html();
  var temp_list = [];

  extract_element_tag(source_html, 'div', 'class="imported"', temp_list)
  extract_element_tag(source_html, 'dt', temp_list)

  console.log(temp_list);
}
