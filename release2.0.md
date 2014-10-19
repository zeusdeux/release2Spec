Release 2.0 spec
================

This shall serve as a detailed specification of all the possible routes in the 2nd version of the application.

## Components overview

- MainAppComponent
    + HeaderComponent
        * LogoComponent
        * AddNewLocationComponent
        * LocationSwitcherComponent
        * NavComponent
    + AppBodyComponent
        * ListingsComponent
        * InteractionsComponent (formerly reviews)
        * RankingsComponent
        * SettingsComponent
        * CheckoutComponent
        * UpgradeComponent
        * IntercomComponent

## Component details

### HeaderComponent

#### LogoComponent

Contains static logo image.

Behaviour:

Holds our logo or any logo for that matter.
Such static, much wow.

Routes:

- GET logo

#### AddNewLocationComponent

Lets the user add a new location

Behaviour:

- Show textbox for business name,(city, state) and close + submit buttons
- Show a list of matching locations once user submits a business name + (city, state)
- Once the user selects a location, add it and navigate to it i.e., update all components to show data for the newly added location

Routes:

- FetchLocationChoicesRoute
    + POST business name and (city, state)
        * On SUCCESS RETURN list of matching businesses
        * On FAILURE ERROR out with a valid http error code (500, 411, 404, etc) and a detailed message. This message will be shown to the user.
- SubmitNewLocationRoute
    + POST new location data (N,A,P)
        * On SUCCESS RETURN HTTP 200 OK
            - This is a signal for all other components to start asking for updated data for themeselves so as to shift the UI into a state that depicts the new location.
        * On FAILURE ERROR out with a valid http error code and a detailed message. This message will be shown to the user.
            - The other components on the page stay in their current state.

#### LocationSwitcherComponent

Lets the user switch to a new location

Behaviour:

- Show the user a searchable dropdown of current locations he has in his account
- When user clicks on a location, switch to that location and update all components in the app to reflect the new location

Routes:

- GetLocationListRoute
    + GET list of locations
        * On SUCCESS RETURN a list a locations to populate the location switcher dropdown component
        * On FAILURE ERROR out with a valid http error code (500, 411, 404, etc) and a detailed message. This message will be shown to the user.
- SwitchToLocationRoute
    + POST ID of location to switch to
        * On SUCCESS RETURN an HTTP 200 OK
            - The component should inform all other components on page to ask for their respective data for the new location that the user has switched to
        * On FAILURE ERROR out with a valid http error code (500, 411, 404, etc) and a detailed message. This message will be shown to the user.
            - The other components on the page should retain their current state.

#### NavComponent

Behaviour:

- Shows the following list of clickables
    + Listings
    + Interactions
    + Rankings
    + Logout
    + Settings
    + Support
    + FAQ

Each clickable in turn updates the respective component.

Routes:

- ActivateListingsComponentRoute
    + Show listings component
- ActivateInteractionsComponentRoute
    + Show interactions component
- ActivateRankingsComponentRoute
    + Show rankings component
- LogoutRoute
    + POST to destroy current user session
        * On SUCCESS redirect to /
        * On FAILURE ERROR out with a valid http error code (500, 411, 404, etc) and a detailed message. This message will be shown to the user. User isn't logged out.
- ActivateSettingsComponentRoute
    + Show settings component
- ActivateSupportComponent
    + Show support component
- ActivateFAQComponent
    + Show FAQ component

#### AppBodyComponent





