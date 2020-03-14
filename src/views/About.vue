<template>
  <v-timeline :dense="$vuetify.breakpoint.smAndDown">
    <v-timeline-item color="purple lighten-2" fill-dot right>
      <!-- เริ่มกรอกข้อมูลฮีโร่-->
      <v-card>
        <v-card-title class="purple lighten-2">
          <v-icon dark size="42" class="mr-4">mdi-angular</v-icon>
          <h2 class="display-1 white--text font-weight-light">Hero Tank</h2>
        </v-card-title>
        <v-container>
          <v-row>
            <v-col
              cols="12"
              md="10"
            >Accountability: Being the primary method of attack from enemies, focusing on protecting your friends because of their high health.</v-col>
            <v-col cols="12" md="10">
              Fighting style with the team :
              Is a battle launcher (Should wait for the team to come first)
              Try to protect And accept attacks from enemies for as long as possible
              Despite receiving a lot of damage But should not put himself to death in vain
              Try to keep an eye on the enemy And tell your teammates what the enemy is doing
            </v-col>
            <v-col class="hidden-sm-and-down text-right" md="2"></v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-timeline-item>

    <v-timeline-item color="amber lighten-1" fill-dot left small>
      <v-card>
        <v-card-title class="amber lighten-1 justify-end">
          <h2 class="display-1 mr-4 white--text font-weight-light">Hero Support</h2>
          <v-icon dark size="42">mdi-needle</v-icon>
        </v-card-title>
        <v-container>
          <v-row>
            <v-col
              cols="12"
              md="8"
            >Duty: To help friends play games easier, such as Keep an eye on where the enemies are. Heal allies use skills to agitate enemies such as stun, slow, mute.</v-col>
            <v-col cols="12" md="10">
              Fighting style with the team : Help support the fight And support all team members
              Help friends in the team not to die.
              Keep an eye on the assassins on the enemy side.
              Try to keep an eye on the enemy And tell your teammates what the enemy is doing
            </v-col>
            <v-icon size="64">mdi-needle</v-icon>
          </v-row>
        </v-container>
      </v-card>
    </v-timeline-item>

    <v-timeline-item color="cyan lighten-1" fill-dot right>
      <v-card>
        <v-card-title class="cyan lighten-1">
          <v-icon class="mr-4" dark size="42">mdi-sword</v-icon>
          <h2 class="display-1 white--text font-weight-light">Hero Fighter</h2>
        </v-card-title>
        <v-container>
          <v-row>
            <v-col
              cols="12"
              md="8"
            >Duty: Be the main player in melee damage. Because it has a high life force And high melee attack power (Has a neutral ability between the tank and the assassin)</v-col>
            <v-col cols="12" md="10">
              Fighting style with the team :
              Try to find the rhythm to attack the main damage of enemies such as damage, Carey and Assassin.
              Supporting the attack And protect the team
              Focus on lane control Create a space for friends to walk in the game.
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-timeline-item>

    <v-timeline-item color="red lighten-1" fill-dot left small>
      <v-card>
        <v-card-title class="red lighten-1 justify-end">
          <h2 class="display-1 mr-4 white--text font-weight-light">Hero Assassin</h2>
          <v-icon dark size="42">mdi-sword-cross</v-icon>
        </v-card-title>
        <v-container>
          <v-row>
            <v-col class="hidden-sm-and-down" md="2">
              <v-icon size="64">mdi-ninja</v-icon>
            </v-col>
            <v-col
              cols="12"
              md="10"
            >Duty: Assassinate the enemy. Focusing on agile movement, with severe melee damage But has a low life force</v-col>
            <v-col cols="12" md="10">
              Fighting style with the team :
              Killing the enemy damage (penetrating)
              Find an area to dodge enemies. Being in a position that is difficult for the enemy to defend
              Try to keep moving To prevent being the target of the enemy
              Watch the rhythm before going into the fight to damage and protect yourself from death.
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-timeline-item>

    <v-timeline-item color="red lighten-2" fill-dot right>
      <v-card>
        <v-card-title class="red lighten-2">
          <v-icon class="mr-4" dark size="42">mdi-pistol</v-icon>
          <h2 class="display-1 white--text font-weight-light">Hero Carry</h2>
        </v-card-title>
        <v-container>
          <v-row>
            <v-col>Duty: Be the main player in intense remote physical damage.</v-col>
            <v-col cols="12" md="10">
              Fighting style with the team :
              Must do the main damage to the team Especially at the end of the game
              Beware of the melee attacks from the opposing Assassin.
              Try to survive until the end of the fight.
              Do not die often because the team will lack damage.
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-timeline-item>
    <v-timeline-item color="green lighten-1" fill-dot right>
      <v-card>
        <v-card-title class="green lighten-1">
          <v-icon class="mr-4" dark size="42">mdi-humble-bundle</v-icon>
          <h2 class="display-1 white--text font-weight-light">Hero Mage</h2>
        </v-card-title>
        <v-container>
          <v-row>
            <v-col>Duty: Damage caused by the back line. Has strong magic attack There is a skill to eliminate the enemy rhythm.</v-col>
            <v-col cols="12" md="10">
              Fighting style with the team :
              Standing behind is the main damage in battle (from a distance)
              Try to use the skills as much as possible, focusing on the enemy Tank and Fighter.
              The rhythm of the fight to be careful of the opposing side.
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-timeline-item>
  </v-timeline>
</template>