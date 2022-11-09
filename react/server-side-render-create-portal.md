The `React` portals do not render on the server, hence, we need to actually collect all the portals that have been created during the execution of `React` code and then attach those portals manually. This trick is not perfect though.

**An exact implementation detail can be found in [this blog](https://michalzalecki.com/render-react-portals-on-the-server/).**
