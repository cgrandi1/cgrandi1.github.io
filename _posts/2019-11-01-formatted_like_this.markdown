---
layout: post
title:      "formatted like this"
date:       2019-11-01 00:49:43 -0400
permalink:  formatted_like_this
---


#This project was particulary difficult as there were files and alot more factors involved. As I describe in my video, I needed to create ajax requests in order to get the JSON data. From there, I had to serialize the JSON data to dsplay in the information I wanted it to render. For my first step, I just simply wanted to post a form using a post request. When that post was displayed, I wanted to do an asynchronous request to display a message at the bottom of the of the new page. In the create controller, in order to create a new league, I had just render JSON. Therefore, I was able to grab just JSON data to display it on the new page. The message that was displayed at the bottom came from my prototype. My constructor had the properities of the object, and my protoype was an an aditional protoype that I could render when called upon. That particular prototype displayed the message: "Good job, you created `${data.name}`. 



```$(function () {
  $('form').submit(function(event) {
    event.preventDefault();

    var values = $(this).serialize();
    var posting = $.post('/leagues', values);

    posting.done(function(data) {
      $("#productResult").append(`<p> Good job, you created ${data.name}!</p>`)
    });
  });
});
```

``` def create
    @league = League.create(league_params)
    @league.user = current_user
    if @league.save
      render json: @league, status: 201
    else
      render :new
    end
  end```

After that message was displayed, you click the "Back to the Leagues" request, where it would send you back to the index page. The index page displayed all the leagues you created. The index page only displayed the name of the league, as well had options of: Creating a new league, More Info, and See League Individually. When you click on the More Info Button it would asynchronously display all the leagues at the bottom of the page. So it would append all the names of the leagues, costs of the leagues, and amount of people in the leagues on the index page. 

```    def index
      @user = current_user
      @leagues = @user.leagues
      respond_to do |form|
        form.html{render :index}
        form.json{render json: @leagues}
      end 
      if @user = session[:id]
        logged_in?
      end 
    end ````

```$(function () {
  $(".js-more").on("click", function(e) {
   e.preventDefault();
      let id = $(this).data("id");
      $.get(`/users/${id}/leagues.json`, function(data){
        let leagues = data
        for(l = 0; l< leagues.length; l++){
          console.log(leagues)
          $('#leagues').append(`<p> League Name: ${leagues[l].name} <br> This league cost's: ${leagues[l].cost} <br> This league has ${leagues[l].people_in_league} people </p>`)
        }
      });
  });
});```

When you click on the See League Individually, it takes you to the show page. In the show page it displays each individual league and their properities. At the bottom of the page, when you click on "When it was the league created", it displays when the league was created. I used the constructor and protopye to disaplyed the time in which the league was created.

```$(function (){
  $(".js-create").on("click", function(e){
    e.preventDefault();
    let id = $(this).data("id");
    $.get(`/leagues/${id}.json`, function(response){
      let newLeague = new League(response)
      let renderPage = newLeague.showHTML();
       $('#createdLeague').html(renderPage)
    });

  });

});```


```class League {
  constructor(obj){
    this.id = obj.id;
    this.name = obj.name;
    this.cost = obj.cost;
    this.people_in_league = obj.people_in_league
    this.created_at = obj.created_at;
  }
}

League.prototype.showHTML = function () {
  return (`<p> Created: ${this.created_at}</p>`)
};```




And when you click on Next team at the top of the page, it's able to show each team without reloading the page, in other words, displays the information asynchronously. 

```  $(function () {
    $(".js-next").on("click", function(event) {
        event.preventDefault();
        var nextId = parseInt($(".js-next").attr("data-id")) + 1;
        $.get("/leagues/" + nextId + ".json", function(data) {
            $(".leagueName").text(data["name"]);
            $(".leagueCost").text(data["cost"]);
            $(".leaguePeopleInLeague").text(data["people_in_league"]);
            $(".js-next").attr("data-id", data["id"]);
      });
    });
  });







		
		
