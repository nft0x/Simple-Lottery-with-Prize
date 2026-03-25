# Simple-Lottery-with-Prize
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SimpleLotteryPrize {
    address[] public players;
    uint256 public ticketPrice = 0.001 ether;

    function buyTicket() public payable {
        require(msg.value == ticketPrice, "Wrong ticket price");
        players.push(msg.sender);
    }

    function pickWinner() public returns (address winner) {
        require(players.length > 0, "No players");
        uint256 index = block.timestamp % players.length;
        winner = players[index];
        payable(winner).transfer(address(this).balance);
        delete players; // reset lottery
    }
}
